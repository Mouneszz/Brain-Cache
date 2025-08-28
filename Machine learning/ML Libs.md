
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






## Visualization

```python
# Survival count
sns.countplot(x='Survived', data=df)
plt.title("Survival Count (0 = No, 1 = Yes)")
plt.show()

# Gender distribution
sns.countplot(x='Sex', data=df)
plt.title("Gender Count")
plt.show()

# Passenger Class distribution
sns.countplot(x='Pclass', data=df)
plt.title("Passenger Class Distribution")
plt.show()



# Survival by Gender
sns.countplot(x='Survived', hue='Sex', data=df)
plt.title("Survival by Gender")
plt.show()

# Survival by Passenger Class
sns.countplot(x='Survived', hue='Pclass', data=df)
plt.title("Survival by Class")
plt.show()

# Survival by Embarkation Port
sns.countplot(x='Survived', hue='Embarked', data=df)
plt.title("Survival by Embarked Port")
plt.show()
```
## Titanic Decision Tree
```python
# Titanic Dataset - Decision Tree Classification

import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import accuracy_score, classification_report

# -----------------
# 1. Load Dataset
# -----------------
df = pd.read_csv("titanic.csv")

# -----------------
# 2. Drop unwanted columns
# -----------------
df.drop(['Name', 'Sex', 'Embarked', 'SibSp', 'Cabin', 'Parch', 'PassengerId'], 
        axis=1, inplace=True)

# -----------------
# 3. Handle missing values
# -----------------
df['Age'].fillna(df['Age'].mean(), inplace=True)   # Replace missing Age with mean

# -----------------
# 4. One-Hot Encoding
# -----------------
df = pd.get_dummies(df, columns=['Sex', 'Embarked'], drop_first=True)  # creates columns like Sex_male, Embarked_Q, etc.

# -----------------
# 5. Define Features and Target
# -----------------
X = df.drop("Survived", axis=1)  # Features
y = df["Survived"]               # Target

# -----------------
# 6. Train-Test Split
# -----------------
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# -----------------
# 7. Train Decision Tree
# -----------------
model = DecisionTreeClassifier(random_state=42)
model.fit(X_train, y_train)

# -----------------
# 8. Evaluate
# -----------------
y_pred = model.predict(X_test)
print("Accuracy:", accuracy_score(y_test, y_pred))
print("Classification Report:\n", classification_report(y_test, y_pred))

```
