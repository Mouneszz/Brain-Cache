



##  Self-Attention for Token _i_ (simple explanation)

- Take the **query of token i** and compare (dot product) with the **keys of all tokens** in the sequence.
    
- Apply **softmax** to these scores to get attention weights that show how much token _i_ should focus on each other token.
    
- Multiply each **value vector** by its attention weight and **sum them all up** → this gives a new context vector for token _i_.
    
- Finally, **add this context vector to the original embedding of token i** (residual connection), so the token keeps both its original meaning and the new contextual meaning.



**Input embedding**
```
X =
[[6 1 4 4]   ← token 1
 [8 4 6 3]]  ← token 2

```
**Matrices of q k v**
```
W_Q =
[[1 4 3 1]
 [1 1 3 2]
 [3 4 4 3]
 [1 2 2 2]]

W_K =
[[2 1 2 1]
 [4 1 4 2]
 [3 4 4 1]
 [3 4 1 2]]

W_V =
[[4 2 4 4]
 [3 4 1 2]
 [2 2 4 1]
 [4 3 1 4]]

```

```
Q1 = [23, 49, 45, 28]  
Q2 = [33, 66, 66, 40]

K =
[[40, 39, 36, 20],   ← K1
 [59, 48, 59, 28]]   ← K2
V =
[[51, 36, 45, 46],   ← V1
 [68, 53, 63, 58]]   ← V2

```

### Step 2. Compute similarity (dot product Q1·Kj)

Q1.Kj
- With K1: `23*40 + 49*39 + 45*36 + 28*20 = 2505.5` (after /√d_k)
- With K2: `23*59 + 49*48 + 45*59 + 28*28 = 3574`
So **scores for token 1** are:

``` `[2505.5, 3574.0]` ```


```
softmax([2505.5, 3574.0]) = [0.0, 1.0]

```

```
Attention for token 1 =
0.0 * V1 + 1.0 * V2
= [68, 53, 63, 58]


```

```
we finaly add the 
X1 + Attention = [6, 1, 4, 4] + [68, 53, 63, 58]
               = [74, 54, 67, 62]

```






---

# 🧠 Transformers — Detailed Notes

## 1. Why Transformers?

- Old models (RNNs, LSTMs) process tokens **sequentially**, making them slow and not great at long-range dependencies.
    
- Transformers process tokens **in parallel**, thanks to the **attention mechanism**.
    
- Key idea: _Each word can look at every other word and decide how important it is._
    

---

## 2. Attention Mechanism (Core Idea)

- Imagine reading: _“The cat sat on the mat.”_
    
- For the word _“sat”_, you don’t just look at it alone. You ask:
    
    - Should I pay attention to _“cat”_ (who sat)?
        
    - Should I pay attention to _“mat”_ (where it sat)?
        
- Attention calculates these **relationships between tokens**.
    

---

## 3. Queries, Keys, and Values

Every token (word embedding) is transformed into three different vectors using learned linear layers:

- **Query (Q):**
    
    - Represents the _question this token is asking_.
        
    - Example: “Who do I need to look at to understand my meaning?”
        
- **Key (K):**
    
    - Represents the _content this token can offer to others_.
        
    - Example: “Here’s what I represent — do you need me?”
        
- **Value (V):**
    
    - Represents the _actual information I’ll contribute if someone attends to me_.
        
    - Example: “Here’s the data you’ll take from me.”
        

👉 In short:

- **Q = what I want**
    
- **K = what I offer**
    
- **V = the info I give when chosen**
    

---

## 4. How Attention Works (Step by Step)

1. **Compare Queries with Keys:**
    
    - For each token, take its Query and compare with every Key (dot product).
        
    - Result = similarity score (how much this token should pay attention to another).
        
2. **Scale and Normalize:**
    
    - Divide scores by dk\sqrt{d_k} (dimension of key).
        
    - Apply **softmax** so scores become probabilities (attention weights).
        
3. **Weighted Sum of Values:**
    
    - Use these weights to combine the Value vectors.
        
    - The result = new representation of the token, enriched with context from other tokens.
        

### Formula:

Attention(Q,K,V)=softmax(QKTdk)V\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V

---

## 5. Multi-Head Attention

- A single attention calculation might capture **only one type of relationship**.
    
- Example: one head focuses on “subject → verb”, another on “word order”, another on “long-distance meaning”.
    
- Multi-Head Attention = run attention **in parallel multiple times** with different learned Q/K/V projections.
    
- Outputs from all heads are concatenated and projected back.
    

---

## 6. Positional Encoding

- Attention treats tokens as a **set** (no order).
    
- But language has **word order**:
    
    - _“dog bites man”_ vs _“man bites dog”_.
        
- Solution: add **positional encodings** to embeddings:
    
    - Sinusoidal (sine & cosine patterns) or learned vectors.
        
    - This gives the model a sense of sequence.
        

---

## 7. Transformer Block

Each layer has two main parts:

1. **Multi-Head Attention** (find context).
    
2. **Feed-Forward Network (FFN)** (apply nonlinear transformations token-wise).
    

Wrapped with:

- **Add & Norm** = residual connection + layer normalization → stabilizes training and preserves info.
    

---

## 8. Encoder–Decoder Structure

- **Encoder:**
    
    - Takes input sequence.
        
    - Produces contextual embeddings (each token knows about others).
        
- **Decoder:**
    
    - Generates output sequence one token at a time.
        
    - Uses **Masked Self-Attention** (can’t peek into the future).
        
    - Also attends to encoder outputs (so translation knows what it’s translating).
        

---

## 9. Intuition Recap

- Attention is like a **smart search system** inside the model.
    
- **Q, K, V** are not literal "questions/answers" — they are **learned vector spaces**.
    
- Model figures out:
    
    - When a token should look at another.
        
    - How much weight to give it.
        
    - What information to borrow.
        

