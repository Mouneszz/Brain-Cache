### **Transformer Block (12 Layers)**

- **Layer Normalization**

- **Dense Layer**


### **Transformer Block Overview**

A Transformer block is a fundamental unit in transformer-based models, designed to process sequential data efficiently. It relies on **self-attention** to understand relationships between words, unlike traditional models that process data sequentially.

#### **Self-Attention Mechanism**

Self-attention helps the model capture relationships between words in a sentence. Since a machine doesn’t understand context the way humans do, self-attention assigns importance to different words using three key components:
     Let’s say we have a sentence:  
      **"The cat sat on the mat."**
  
Query (Q) → "What should I focus on?"
Example: "sat" wants to know which words are important to it.
Key (K) → "Which words are important?"
Example: "cat" might be important for "sat" because "the cat sat."
Value (V) → The actual meaning of the words.
Example:
"Cat" is an animal, "Sat" is an action (verb), "Mat" is an object.

- **Dense Layer** → Combines everything and refines the output.

### **Embedding Matrix**

- Converts words into numerical representations (vectors).
- A matrix is created with words on the **y-axis**, and similarity between words is captured in the values.

### **Positional Encoding**

- Since word order matters, **positional encoding** assigns weights based on the word’s position in the sentence.
- Two identical words appearing in different positions will have different encodings.


- The final representation is computed as:
	Q=Embedding Matrix × Positional Encoding

This ensures that the transformer understands **both** word meanings and their positions in the sentence.

```
Example: "Cat" as Query
If "cat" is the current focus (Query):

It compares Q_cat with all Keys (K_the, K_cat, K_sat, K_on, K_mat).

It finds high similarity with "sat" and "mat" (because they are contextually related).

It then uses Values (V) of "sat" and "mat" to update the word representation of "cat".

Similarly, if "mat" is the focus (Query):

 - It compares Q_mat with all Keys.

 - It might find "on" or "sat" more relevant.

 - It retrieves information from their Values (V_on, V_sat).
```
