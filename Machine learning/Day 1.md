Perfect 👌 Let’s create **Day 1 – Linear Algebra Notes (for ML & Interview Revision)**.

---

# 📘 Day 1 – Linear Algebra Notes

### 1. **Vectors**

- A **vector** is an ordered list of numbers (e.g., [2,3][2, 3], [1,5,−2][1, 5, -2]).
    
- Represents **magnitude and direction** in space.
    
- Example: [3,4][3, 4] → move 3 units in x, 4 units in y.
    
- In ML, a vector can represent **features of data** (e.g., [height, weight, age]).
    

---

### 2. **Matrices**

- A **matrix** is a rectangular array of numbers arranged in rows & columns.
    
- Example:
    
    A=[1234]A = \begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix}
- Can represent **multiple vectors** or a **transformation**.
    
- In ML:
    
    - Input dataset → stored as a matrix (rows = samples, columns = features).
        
    - Transformation (rotation, scaling, projection) → matrix multiplication.
        

---

### 3. **Linear Transformations**

- A **linear transformation** is a function that transforms vectors but preserves:
    
    - **Linearity** (scaling and addition).
        
    - Example: T(x)=AxT(x) = Ax where AA is a matrix.
        
- Common transformations:
    
    - **Scaling** → enlarges/shrinks vectors.
        
    - **Rotation** → rotates vectors in space.
        
    - **Projection** → projects onto a line/plane.
        
- In ML: Used in embeddings, feature transformation, and neural nets.
    

---

### 4. **Matrix-Vector Multiplication**

- Multiply a matrix by a vector to get a **new transformed vector**.
    
- Example:
    
    A=[2003],x=[12]A = \begin{bmatrix}2 & 0 \\ 0 & 3\end{bmatrix}, \quad x = \begin{bmatrix}1 \\ 2\end{bmatrix} Ax=[2003][12]=[26]Ax = \begin{bmatrix}2 & 0 \\ 0 & 3\end{bmatrix}\begin{bmatrix}1 \\ 2\end{bmatrix} = \begin{bmatrix}2 \\ 6\end{bmatrix}
- Interpretation → scaling x by 2, y by 3.
    

---

### 5. **Dot Product**

- For vectors a=[a1,a2]a = [a_1, a_2], b=[b1,b2]b = [b_1, b_2]:
    
    a⋅b=a1b1+a2b2a \cdot b = a_1b_1 + a_2b_2
- Measures **similarity** between vectors.
    
    - If a⋅b>0a \cdot b > 0 → pointing in similar directions.
        
    - If a⋅b=0a \cdot b = 0 → orthogonal (perpendicular).
        
    - If a⋅b<0a \cdot b < 0 → pointing in opposite directions.
        
- In ML: Used in **cosine similarity, embeddings, attention in transformers**.
    

---

### 6. **Norms (Vector Length)**

- **Norm** = measure of vector magnitude/length.
    
- Common norm:
    
    - **L2 norm (Euclidean)**:
        
        ∣∣x∣∣2=x12+x22+⋯+xn2||x||_2 = \sqrt{x_1^2 + x_2^2 + \dots + x_n^2}
- In ML: Used in **regularization** (L2 penalty in regression, weight decay in deep learning).
    

---

### 7. **Orthogonality**

- Two vectors are **orthogonal** if their dot product = 0.
    
- Means they are **perpendicular**, i.e., carry **independent information**.
    
- In ML: Important in **PCA (Principal Component Analysis)** and **orthogonal features**.
    

**Eigenvectors**
These are the vectors that do not change their direction when a linear transformation/matrix is applied to them.
- Only stretched or shrink (magnitude) not the direction
- The scaled value is called as **Eigenvalue**

