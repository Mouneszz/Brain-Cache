## CNN (Convolutional Neural Network)
- It is Deep learning architecture which is used for image recognition and other spatial identification

### Core Building Blocks
- Convolutional Layer
	Detect features (edges, corners, textures) by sliding small filters (kernels) over the input.
	A kernel is usually `3×3` or `5×5`.It slides across the image, multiplying values and summing them (dot product).


- Activation Function (usually ReLU)
	- After convolution, we pass the result through a **non-linearity**.
	- It removes negative values, adds non-linearity, and makes training faster.

- Pooling Layer
	- Reduce spatial size while keeping important information.
	- **Max pooling:** keeps the max value in each region (most common)
	- Reduces computation, Makes model invariant to small translations ,Helps prevent overfitting

- Fully Connected (Dense) Layer
	-  In later stages, you flatten the pooled feature maps and connect to a **fully connected** layer.
	- This part combines detected features into final decisions (classification, regression, etc.).


```python
Conv2D(32, kernel_size=(3, 3), activation='relu')
```
In the above conv layer 32 refers to the number of filter/kernels which slides over the image and detect the specific pattern
- the first layer will learn basic 32 pattern in the image (ex edges, corners)

we do it until the filter count reaches 512
After that we have to flatten and dense(connect them into )
```python
flatten()
```
This flattens convert the output of `6 x 6 x 256`  3D vector into `9216` 1D vector

```python
Dense(512, activation='relu')
```
This maps the 9216 features into 512 high level combinations
- Each 512 neurons have 9216 input

```python
Dense(7,activation='softmax')
```
this line converts the 512 features 7 neurons(7 type of emotions )
- `softmax`  converts the 7  into numbers which we can sum up to 1.

