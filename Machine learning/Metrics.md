# 🔹 1. **Accuracy**
- Proportion of correctly classified samples.
- Formula:
    `Accuracy = (TP + TN) / (TP + TN + FP + FN)`
- Good when classes are balanced.

```python 
from sklearn.metrics import accuracy_score
accuracy_score(y_test, y_pred)
```
---
# 🔹 2. **Confusion Matrix**
- Table showing correct & wrong predictions **per class**.
- Terms:
    - **TP (True Positive)** = correctly predicted positive
    - **TN (True Negative)** = correctly predicted negative
    - **FP (False Positive)** = wrongly predicted positive
    - **FN (False Negative)** = wrongly predicted negative
    
```python
from sklearn.metrics import confusion_matrix
confusion_matrix(y_test, y_pred)
```

---
# Classification Report

```python
from sklearn.metrics import classification_report print(classification_report(y_test, y_pred))

# Output
              precision    recall  f1-score   support

           0       0.97      0.97      0.97        33
           1       0.96      0.96      0.96        28
           2       0.91      0.94      0.93        33
           3       0.92      0.97      0.94        34
           4       1.00      0.98      0.99        46
           5       0.93      0.91      0.92        47
           6       0.97      0.97      0.97        35
           7       1.00      0.97      0.99        34
           8       0.94      0.97      0.95        30
           9       0.95      0.93      0.94        40

    accuracy                           0.96       360
   macro avg       0.96      0.96      0.96       360
weighted avg       0.96      0.96      0.96       360
```

### **Precision**
- Out of all predicted positives, how many are actually positive?
- Formula:
    `Precision = TP / (TP + FP)`
- Good when **false positives** are costly (e.g., spam filter).
### **Recall (Sensitivity / TPR)**

- Out of all actual positives, how many did we catch?
- Formula:
    `Recall = TP / (TP + FN)`
- Good when **false negatives** are costly (e.g., disease detection).
### **F1 Score**
- Harmonic mean of Precision & Recall.
- Formula:
    `F1 = 2 * (Precision * Recall) / (Precision + Recall)`
- Good for **imbalanced datasets**.
