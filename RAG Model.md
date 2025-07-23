## 🎯 **What is RAG?**

> **RAG** combines information retrieval with a language model to improve accuracy and reduce hallucination.  
> It retrieves relevant documents using semantic search, then feeds them to a language model to generate accurate answers.

⚙️ **Main Components Used in My RAG Setup**
###  1. **Vector Store (FAISS)**

- Stores dense vector embeddings.
- Fast similarity search over high-dimensional vectors.
- You must **encode both your documents and your query** using the **same embedding model**.
	```python
import faiss
index = faiss.read_index("college_index.faiss")
```
### 2. **Document Chunks (Pickle)**

- Stored in `college_texts.pkl`
- Contains department data or metadata corresponding to each vector in FAISS.
```python
import pickle
with open("college_texts.pkl", "rb") as f:
    chunks = pickle.load(f)
```
###  3. **Embedding Model**

- `all-MiniLM-L6-v2` from `sentence-transformers`
- Used to convert both queries and documents to vectors.
```python
from sentence_transformers import SentenceTransformer
model = SentenceTransformer("all-MiniLM-L6-v2")
query_vector = model.encode(query).reshape(1, -1)
```

###  4. **Retrieval Step**

- Perform FAISS similarity search to get top `k` most relevant chunks:
```python
D, I = index.search(query_vector, k)
results = [chunks[i] for i in I[0]]
```

🧠 **RAG Flow Summary**
```text
1. User asks a question (query).
2. Convert query to vector using the same model used during indexing.
3. Use FAISS to find top-k relevant document vectors.
4. Retrieve original chunks using pickle data.
5. Combine results and pass them to LLM (like GPT).
```

