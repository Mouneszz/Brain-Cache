**Bias:** 
- **Bias** is the **error due to overly simplistic assumptions** in a model.
- It measures how far the model’s predictions are from the actual values on average.
	
**Variance**
- So if a model is well trained in training dataset but for testing it performs very bad it have high Variance, it causes Overfitting.
- 
- **Variance** is the **error due to model sensitivity to small changes in the training data**.
- High variance → model **fits the training data very closely** but may fail on unseen data.

**Cross Validation**
- When you want to train a model but you have so many choices like linear,svm etc..
- So for example w have a training dataset we usually train that in the ratio of `80:20` .By using **Cross Validation** we **Train** and **Test** all the models with with **all the combination** of `80:20` and get the how many got correct and wrong 
- we choose the model with the lowest wrongs.

### Ridge Regression 
- So Imagine we have Less training data if we train it with a linear regression  it may fit perfect with zero **Bias** but while testing the **variance** would be so high to solve this problem we create this the fit somewhat not perfect with Extra Bias

**Ridge regression** is a form of **regularized linear regression** that adds a penalty to the model's coefficients to reduce overfitting. It introduces a slight **bias** but significantly lowers **variance**, leading to better generalization
- 