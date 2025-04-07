```python
import tensorflow as tf
from tensorflow.keras.layers import Layer, Dense, LayerNormalization, Dropout, Embedding
from tensorflow.keras import Model

class MultiheadAttention(Layer):
    def __init__(self, embed_dim, num_heads):
        super().__init__()
        self.embed_dim = embed_dim
        self.num_heads = num_heads
        self.attention_dim = embed_dim // num_heads
        self.wq = Dense(embed_dim)
        self.wk = Dense(embed_dim)
        self.wv = Dense(embed_dim)
        self.dense = Dense(embed_dim)

    def split_heads(self, x, batch_size):
        x = tf.reshape(x, (batch_size, -1, self.num_heads, self.attention_dim))
        return tf.transpose(x, perm=[0, 2, 1, 3])

    def call(self, q, k, v, mask=None, training=False):
        batch_size = tf.shape(q)[0]
        q = self.split_heads(self.wq(q), batch_size)
        k = self.split_heads(self.wk(k), batch_size)
        v = self.split_heads(self.wv(v), batch_size)

        matmul_qk = tf.matmul(q, k, transpose_b=True)
        dk = tf.cast(tf.shape(k)[-1], tf.float32)
        scaled_attention_logits = matmul_qk / tf.math.sqrt(dk)

        if mask is not None:
            scaled_attention_logits += (mask * -1e9)

        attention_weights = tf.nn.softmax(scaled_attention_logits, axis=-1)
        output = tf.matmul(attention_weights, v)
        output = tf.transpose(output, perm=[0, 2, 1, 3])
        concat_attention = tf.reshape(output, (batch_size, -1, self.embed_dim))
        return self.dense(concat_attention)

class FeedForwardNetwork(Layer):
    def __init__(self, embed_dim, dff):
        super().__init__()
        self.dense1 = Dense(dff, activation='relu')
        self.dense2 = Dense(embed_dim)

    def call(self, x):
        return self.dense2(self.dense1(x))

class TransformerBlock(Layer):
    def __init__(self, embed_dim, num_heads, dff, dropout_rate=0.1):
        super().__init__()
        self.att = MultiheadAttention(embed_dim, num_heads)
        self.ffn = FeedForwardNetwork(embed_dim, dff)
        self.norm1 = LayerNormalization(epsilon=1e-6)
        self.norm2 = LayerNormalization(epsilon=1e-6)
        self.dropout1 = Dropout(dropout_rate)
        self.dropout2 = Dropout(dropout_rate)

    def call(self, x, mask=None, training=False):
        attn_output = self.att(x, x, x, mask, training=training)
        attn_output = self.dropout1(attn_output, training=training)
        out1 = self.norm1(x + attn_output)
        ffn_output = self.ffn(out1)
        ffn_output = self.dropout2(ffn_output, training=training)
        return self.norm2(out1 + ffn_output)

class GPT2(Model):
    def __init__(self, vocab_size, embed_dim=768, num_heads=12, dff=3072, num_layer=12, dropout_rate=0.1):
        super().__init__()
        self.token_emb = Embedding(vocab_size, embed_dim)
        self.pos_emb = Embedding(2048, embed_dim)
        self.transformer_blocks = [TransformerBlock(embed_dim, num_heads, dff, dropout_rate) for _ in range(num_layer)]
        self.norm = LayerNormalization(epsilon=1e-6)
        self.out = Dense(vocab_size)

    def create_casual_mask(self, seq_len, batch_size):
        mask = tf.linalg.band_part(tf.ones((seq_len, seq_len)), -1, 0)
        return tf.expand_dims(mask, axis=0)  # Shape: (1, seq_len, seq_len)

    def call(self, x, training=False):
        batch_size = tf.shape(x)[0]
        seq_len = tf.shape(x)[1]
        casual_mask = self.create_casual_mask(seq_len, batch_size)

        token_embeddings = self.token_emb(x)
        pos_embeddings = self.pos_emb(tf.range(seq_len)[:, tf.newaxis])
        x = token_embeddings + pos_embeddings

        for transformer in self.transformer_blocks:
            x = transformer(x, casual_mask, training=training)

        x = self.norm(x)
        return self.out(x)

# Define model
VOCAB_SIZE = 50256
MAX_LENGTH = 1024

inputs = tf.keras.layers.Input(shape=(MAX_LENGTH,), dtype=tf.int32)
outputs = GPT2(vocab_size=VOCAB_SIZE)(inputs)
gpt2 = Model(inputs, outputs)

# Model Summary
gpt2.summary()
```