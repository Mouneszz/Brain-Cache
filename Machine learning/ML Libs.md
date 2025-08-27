
### 📌 **NumPy (np)**

```python
import numpy as np

# Array creation
a = np.array([1, 2, 3])             # 1D array
b = np.zeros((2, 3))                 # 2x3 zeros
c = np.ones((3, 3))                  # 3x3 ones
d = np.arange(0, 10, 2)              # [0,2,4,6,8]
e = np.linspace(0, 1, 5)             # [0,0.25,0.5,0.75,1]

# Shape & Reshape
a.shape                              
a.reshape(3, 1)                      

# Indexing & Slicing
a[0], a[-1]
a[1:3]

# Math operations
np.mean(a), np.std(a), np.var(a)
np.sum(a), np.min(a), np.max(a)
np.dot(a, a)                         # dot product
np.linalg.inv(np.eye(3))             # inverse matrix

# Random
np.random.rand(3, 3)
np.random.randn(3, 3)
np.random.randint(0, 10, (2, 2))
```

---

### 📌 **Pandas (pd)**

```python
import pandas as pd

# Read / Write
df = pd.read_csv("data.csv")
df.to_csv("out.csv", index=False)

# Explore
df.head(), df.tail()
df.info()
df.describe()

# Selection
df["col"]              # single column
df[["col1", "col2"]]   # multiple columns
df.iloc[0, 1]          # row & col by index
df.loc[0, "col"]       # row & col by label

# Filtering
df[df["col"] > 5]
df[(df["col1"] > 5) & (df["col2"] < 3)]

# Operations
df["new"] = df["col1"] + df["col2"]
df.drop("col", axis=1, inplace=True)
df.rename(columns={"old": "new"}, inplace=True)
df.fillna(0)
df.dropna()

# Grouping & Aggregation
df.groupby("category")["value"].mean()
df["col"].value_counts()

# Encoding
pd.get_dummies(df["cat_col"])
```

---

### 📌 **Matplotlib (plt)**

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4]
y = [10, 20, 25, 30]

plt.plot(x, y, label="line")   # line plot
plt.scatter(x, y, label="scatter")  # scatter
plt.bar(x, y)                  # bar
plt.hist(y, bins=5)             # histogram

plt.xlabel("X-axis")
plt.ylabel("Y-axis")
plt.title("My Plot")
plt.legend()
plt.show()
```

---

### 📌 **Seaborn (sns)**

```python
import seaborn as sns
import matplotlib.pyplot as plt

# Built-in datasets
df = sns.load_dataset("iris")

# Basic plots
sns.scatterplot(x="sepal_length", y="sepal_width", hue="species", data=df)
sns.histplot(df["sepal_length"], kde=True)
sns.boxplot(x="species", y="sepal_length", data=df)
sns.heatmap(df.corr(), annot=True, cmap="coolwarm")

plt.show()
```

---

### 📌 **Scikit-learn (sklearn)**

```python
from sklearn.model_selection import train_test_split, cross_val_score
from sklearn.preprocessing import StandardScaler, MinMaxScaler, LabelEncoder
from sklearn.linear_model import LinearRegression, LogisticRegression
from sklearn.tree import DecisionTreeClassifier
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score, confusion_matrix, classification_report

# Train-test split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# Preprocessing
scaler = StandardScaler()
X_train = scaler.fit_transform(X_train)
X_test = scaler.transform(X_test)

# Encoding
le = LabelEncoder()
y = le.fit_transform(y)

# Model
model = LogisticRegression()
model.fit(X_train, y_train)

# Prediction
y_pred = model.predict(X_test)

# Evaluation
accuracy_score(y_test, y_pred)
confusion_matrix(y_test, y_pred)
classification_report(y_test, y_pred)
```
