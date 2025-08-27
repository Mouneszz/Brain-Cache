
## 1. Linear Regression

- **Definition**: Predicts a continuous value (e.g., house price, salary).
    
- **Equation**:
    
    y=w1x1+w2x2+...+wnxn+by = w_1x_1 + w_2x_2 + ... + w_nx_n + b
    - wiw_i: weights/coefficients
        
    - bb: bias/intercept
        
- **Goal**: Minimize error → usually **Mean Squared Error (MSE)**:
    
    MSE=1n∑(ypred−ytrue)2\text{MSE} = \frac{1}{n}\sum (y_{pred} - y_{true})^2
- **Learning**: Gradient Descent updates weights:
    
    w=w−α⋅∂Loss∂ww = w - \alpha \cdot \frac{\partial \text{Loss}}{\partial w}
    
    where α\alpha = learning rate.
    
- **Use case**: Predicting sales, temperature, stock prices, etc.
    

---

## 2. Logistic Regression

- **Definition**: Classification algorithm (not regression!) → predicts **probability** of belonging to a class.
    
- **Sigmoid Function**:
    
    σ(z)=11+e−z\sigma(z) = \frac{1}{1 + e^{-z}}
    - Maps any value to range [0,1][0,1].
        
    - z=w1x1+...+wnxn+bz = w_1x_1 + ... + w_nx_n + b.
        
- **Decision Rule**:
    
    - If σ(z)≥0.5\sigma(z) \geq 0.5 → Class 1
        
    - Else → Class 0
        
- **Loss Function**: Binary Cross-Entropy:
    
    L=−1n∑[ylog⁡(y^)+(1−y)log⁡(1−y^)]L = -\frac{1}{n}\sum \big[ y\log(\hat{y}) + (1-y)\log(1-\hat{y}) \big]
- **Why not Linear Regression for classification?**
    
    - Linear outputs unbounded values (−∞ to +∞).
        
    - Logistic ensures probabilities between 0 and 1.
        
- **Use case**: Spam detection, fraud detection, yes/no predictions.
    

---

## 3. Key Differences

|Feature|Linear Regression|Logistic Regression|
|---|---|---|
|Output|Continuous value|Probability (0–1)|
|Function|Linear line|Sigmoid curve|
|Loss|MSE|Cross-Entropy|
|Problem type|Regression|Classification|

---

✅ **Quick Example**:

- Predicting house price → **Linear Regression**
    
- Predicting if house is expensive (Yes/No) → **Logistic Regression**
    

---

Would you like me to also prepare **short Python code examples** for both (so you can revise with coding tomorrow before moving to Day 3)?