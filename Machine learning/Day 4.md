
# 🌟 Neural Network Flow in PyTorch

## 1. **Dataset & Dataloader**

- In ML, data is often large → we don’t load all at once.
- **`Dataset`** → defines how to access individual samples (image, label).
- **`DataLoader`** → wraps Dataset, gives batches, shuffles, and loads in parallel.
```python
from torch.utils.data import DataLoader
train_loader = DataLoader(train_dataset, batch_size=64, shuffle=True)

data_iter = iter(train_loader)
images, labels = next(data_iter)   # images: [64, 1, 28, 28], labels: [64]
```

👉 Data is always in form `(inputs, labels)`.
- Inputs → tensors (features, like pixels).
- Labels → ground truth (like class index).
## 2. **Model (Neural Network Skeleton)**
We build a model by subclassing `nn.Module`.
### (a) Custom Model

```python
import torch.nn as nn

class MyNet(nn.Module):
    def __init__(self):
        super(MyNet, self).__init__()
        self.fc1 = nn.Linear(28*28, 128)   # input → hidden
        self.fc2 = nn.Linear(128, 10)      # hidden → output

    def forward(self, x):
        x = x.view(x.size(0), -1)          # flatten [batch, 1,28,28] → [batch, 784]
        x = torch.relu(self.fc1(x))        # activation
        x = self.fc2(x)                    # raw scores (logits)
        return x
```
### (b) Sequential Model
Alternative shorthand using `nn.Sequential`:
```python
model = nn.Sequential(
    nn.Flatten(),
    nn.Linear(28*28, 128),
    nn.ReLU(),
    nn.Linear(128, 10)
)
```

👉 Both do the same. Sequential is compact. Custom class gives flexibility.
## 3. **Layers & Computation**

- In ML, we pick pre-built models (SVM, KNN, etc.).
- In DL, we build **layer by layer skeleton**:
    - **`nn.Linear`** → Fully connected layer (matrix multiply + bias).
    - **Activations** (ReLU, Sigmoid, Softmax, etc.) → add non-linearity.
    - **Convolution, Dropout, Pooling** → other layers.

**Computation happens in the `forward()` pass**.
- Input tensor goes through each layer.
- Layers are just mathematical functions (matrix multiplications + activations).

## 4. **Loss Function**
- Measures how far predictions are from labels.
- Example:

```python
criterion = nn.CrossEntropyLoss()
```
For classification:
- Input: raw scores from model `[batch, classes]`.
- Target: class labels `[batch]`.
- Output: scalar loss.
## 5. **Optimizer**

- Updates weights using gradients.
```python
import torch.optim as optim
optimizer = optim.SGD(model.parameters(), lr=0.01)
```

## 6. **Training Loop**

Steps per batch:
1. Get batch → `images, labels`.
2. Forward pass → `outputs = model(images)`.
3. Compute loss → `loss = criterion(outputs, labels)`.
4. Backward pass → `loss.backward()`.
5. Update weights → `optimizer.step()`.
6. Reset gradients → `optimizer.zero_grad()`.

```python
for epoch in range(num_epochs):
    for images, labels in train_loader:
        outputs = model(images)
        loss = criterion(outputs, labels)

        optimizer.zero_grad()   # clear old gradients
        loss.backward()         # compute gradients
        optimizer.step()        # update weights
```

---
## 7. **Evaluation**
- Switch model to eval mode: `model.eval()`.
- Disable gradients:

```python
with torch.no_grad():
    outputs = model(images)
```
- Compare predictions vs labels.

---

## 🔄 Flow Recap

1. **Data** → `Dataset` & `DataLoader`.
2. **Model skeleton** → layers (`nn.Linear`, `nn.Conv2d`, etc.).
3. **Forward pass** → input flows through layers.
4. **Loss function** → compares predictions with labels.
5. **Backward pass** → compute gradients (autograd).
6. **Optimizer step** → update weights.
7. Repeat for many epochs.
