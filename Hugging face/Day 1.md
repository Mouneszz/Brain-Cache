**Hugging Face**
- It is a open source platform and libraries to make our ml/nlp projects development easy.
- - It’s like the **“GitHub + App Store” for AI models**.
- Developers can **download** pretrained models, **fine-tune** them, and **upload** their own models for others to use.

*Main components in hugging face*
- Transformers Library - Bert,GPT-2
- Datasets Library
- Tokenizers
- Hugging Face Hub
- Spaces

   BERT (==Bidirectional Encoder Representations from Transformers==) is a Google-developed language model that improves Natural Language Processing (NLP) by understanding word context bidirectionally, meaning it considers words both before and after a target word in a sentence.
   
   GPT, or Generative Pretrained Transformer, is ==a type of artificial intelligence model designed to understand and generate human-like text and other content==. It uses a "transformer" architecture to process sequential data like language, is "pre-trained" on vast amounts of text data, and is "generative" because it creates new content based on the input it receives.
   
**Transformer**
- A **Transformer** is a type of **deep learning/neural network model architecture** introduced in the paper _“Attention is All You Need” (2017)_.
- Before Transformers RNN were used commonly  but they are sequential in nature
- The main block in the transformer is *Self attention*.


A Transformer has two main parts:
1. **Encoder** → reads input text and builds context (used in BERT).
2. **Decoder** → generates text step by step (used in GPT).
   - **BERT** = Encoder-only (great for classification, sentiment analysis).
   - **GPT** = Decoder-only (great for text generation).  

# . Why are Transformers better?

✅ Can process entire sentences **in parallel** (faster than RNNs).  
✅ Handle **long-range dependencies** better.  
✅ Achieve **state-of-the-art results** in almost every NLP task.  
✅ Easily pretrained on massive data and fine-tuned for specific tasks.

So for a model there are multiples steps in it
- Tokenization 
- Model/Processing
- Decoding/Output
`Hugging face combines them all into a function` *pipeline()*

## `Raw Text → Tokenizer → Transformer Model → Output → Human-readable Result`


```python
## basic integration of mdoel using pipeline 
from transformers import pipeline

classifier = pipeline("sentiment-analysis")

result = classifier("I love gammig")
print(result)
```
Here the pipeline packs all components which is used for a sentiment analysis like:
- Tokenize input
- Pass through model
- Get raw logits
- Apply softmax → get probabilities