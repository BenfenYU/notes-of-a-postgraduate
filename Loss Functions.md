# Loss Functions

## Regression

### Mean Squared Error Loss

The squaring means that larger mistakes result in more error than  smaller mistakes, meaning that the model is punished for making larger  mistakes.

### Mean Squared Logarithmic Error Loss

first calculate the natural logarithm of each of the predicted values, then calculate the mean squared error. It has the effect of relaxing the punishing effect of large differences in large predicted values.

### Mean Absolute Error Loss

On some regression problems, the distribution of the target variable  may be mostly Gaussian, but may have outliers, e.g. large or small  values far from the mean value.

The Mean Absolute Error, or MAE, loss is an appropriate loss function in this case as it is more robust to outliers. It is calculated as the  average of the absolute difference between the actual and predicted  values.

## Binary Classification

### Binary Cross-Entropy Loss

[Cross-entropy](https://machinelearningmastery.com/cross-entropy-for-machine-learning/) is the default loss function to use for binary classification problems.

Mathematically, it is the preferred loss function under the inference  framework of maximum likelihood. It is the loss function to be evaluated first and only changed if you have a good reason.

### Hinge Loss

An alternative to cross-entropy for binary classification problems is the [hinge loss function](https://en.wikipedia.org/wiki/Hinge_loss), primarily developed for use with Support Vector Machine (SVM) models.

### Squared Hinge Loss

simply calculates the square of the score hinge loss. It has the effect  of smoothing the surface of the error function and making it numerically easier to work with.

## Multi-Class Classification

### Multi-Class Cross-Entropy Loss

[Cross-entropy](https://en.wikipedia.org/wiki/Cross_entropy) is the default loss function to use for multi-class classification problems. The function requires that the output layer is configured with an *n* nodes (one for each class), in this case three nodes, and a ‘*softmax*‘ activation in order to predict the probability for each class.

### Sparse Multiclass Cross-Entropy Loss

For example, predicting words in a vocabulary may have tens or hundreds  of thousands of categories, one for each label. This can mean that the  target element of each training example may require a one hot encoded  vector with tens or hundreds of thousands of zero values, requiring  significant memory. 

Sparse cross-entropy addresses this by performing the same cross-entropy calculation of error, without requiring that the target variable be one hot encoded prior to training.

### Kullback Leibler Divergence Loss

[Kullback Leibler Divergence](https://en.wikipedia.org/wiki/Kullback–Leibler_divergence), or KL Divergence for short, is a measure of how one probability distribution differs from a baseline distribution.

As such, the KL divergence loss function is more commonly used when  using models that learn to approximate a more complex function than  simply multi-class classification, such as in the case of an autoencoder used for learning a dense feature representation under a model that  must reconstruct the original input. In this case, KL divergence loss  would be preferred. Nevertheless, it can be used for multi-class  classification, in which case it is functionally equivalent to  multi-class cross-entropy.

