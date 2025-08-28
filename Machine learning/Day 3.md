
## 🌳 Decision Trees & Random Forests

Decision Trees split the dataset based on features using criteria like **Gini Index** or **Entropy** (information gain). They are easy to interpret and visualize but tend to **overfit** if not pruned.

Random Forests solve this by combining many trees using **bagging (bootstrap sampling)** and **ensembling**. Each tree is trained on a random subset of data, and the final prediction is made by majority voting (classification) or averaging (regression). They reduce variance and improve robustness but are less interpretable compared to a single tree.

```python
from sklearn.tree import DecisionTreeClassifier
from sklearn.ensemble import RandomForestClassifier
```

---

## ⚡ Support Vector Machines (SVM)

SVMs work by finding the **optimal hyperplane** that separates classes while maximizing the **margin** between them. The data points closest to the boundary are called **support vectors**.

When data is not linearly separable, the **kernel trick** (e.g., RBF, polynomial, linear) maps data into higher dimensions where separation is easier. SVMs are effective in **text classification, image recognition**, and generally work well on **small to medium-sized datasets**.

```python
from sklearn.svm import SVC
```

---

## 👥 K-Nearest Neighbors (KNN)

KNN is a simple, instance-based learning algorithm. To classify a new point, it looks at the **k nearest neighbors** (based on a distance metric like Euclidean, Manhattan, or Minkowski) and assigns the majority class among them.

The choice of **k** is important:

- Small k → low bias, high variance (more sensitive to noise).
    
- Large k → high bias, low variance (smoother decision boundary).
    

```python
from sklearn.neighbors import KNeighborsClassifier
```

---

## 📉 Principal Component Analysis (PCA)

PCA is a **dimensionality reduction** technique. It projects data into fewer dimensions while retaining as much **variance** as possible. This is done by computing the **eigenvectors and eigenvalues** of the covariance matrix and selecting the top principal components.

PCA is useful for **high-dimensional datasets** (like images or text), reducing noise, and speeding up training without losing much information.

```python
from sklearn.decomposition import PCA
```

---
