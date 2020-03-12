# [Batch Normalization: Accelerating Deep Network Training by Reducing Internal Covariate Shift](https://arxiv.org/pdf/1502.03167.pdf)

**Authors**: Sergey Ioffe, Christian Szegedy

### Problem it addresses

* During training of deep neural networks the distribution of each layer's inputs changes (due to changes of parameters of previous layers).
* Due to this parameter initialization becomes particularly important and as training goes on, smaller learning rates are required (which slows training).
* __Training neural networks whose activation functions have saturating nonlinearities leads to model parameters suffering from _internal covariate shift_. This paper addresses this issues by normalizing layer inputs.__
* Functions with saturating nonlinearities will push many dimensions of the input into the saturated areas of the nonlinearities which will slow convergence.

### Important terminology

* __covariate shift__: the input distribution of a learning system has changed (during training) [Shimodaira, 2000](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.370.4921&rep=rep1&type=pdf)
* __internal covariate shift__: the distribution of network activations changes during training due to a changes in network parameters
* __saturating nonlinearity__: function that has a linear region within its limits. The issue is that inputs that exceed a certain limit are mapped to a constant output.

### Benefits of method

* Parameter initialization is less important.
* Comparatively higher learning rates can be used during training.
* Method acts as a regularizer (in certain cases eliminating the need for Dropout).
* Reduces the dependence of training gradients on the scale of the inputs and their initial values.


### Contributions

* Method normalizes inputs to layers such that their mean and variance is fixed during training. Each standardization is independent, and the mean and variance are computed over the training set.
* To ensure that the normalization does not push the values into the saturated area of the following nonlinearity (e.g. Sigmoid) a pair of parameters is introduced to scale and shift the normalized values. These parameters are learnt alongside the other network parameters.
* For each dimension the variance is computed independently as the size of the batch from which the mean and variance are estimated (to be used in standardization) is likely to be smaller than the number of dimensions. Thus, if a covariance would be computed instead it would result in singular covariance matrices (implying linearity between variables) instead. 
* Method addresses issues of exploding or vanishing gradients. As by normalizing inputs to each layer, small changes to parameters do not get amplified by large scales of inputs.
* Prevents training from getting stuck in the saturated regions of nonlinearities, both through the normalization and by using a shift and scale to ensure the original geometry of the features is preserved.
* [LeCun et.al.](http://yann.lecun.com/exdb/publis/pdf/raiko-aistats-12.pdf) and [Wiesler and Ney](https://papers.nips.cc/paper/4421-a-convergence-analysis-of-log-linear-training.pdf) showed that training converges faster if the network has its inputs whitened (decorrelated, and have zero mean and unit variance). This method whitens the inputs for each layer.