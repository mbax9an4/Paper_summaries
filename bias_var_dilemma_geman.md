Neural Networks and the Bias-Variance Dilemma

Stuart Geman, Elie Bienenstock, and Rene Doursat, 1992

* They suggest that the fundamental challenges in neural modelling are related to representation rather than learning.
* They show that neural network models can be formulated as nonlinear regression problems.
* They focus on the limitations of nonparameteric models, expressing these limitations in terms of the bias/variance dilemma.
    * nonparametric models: statistical models that are not based solely on parametrized distributions (i.e. either distribution free or having a specified distribution with unspecified parameters)
* They bias-variance dilemma is:
    * the estimation error can be decomposed into two terms, one relating to the bias of the model and the other to its variance
    * this means that either the bias or the variance can be the source of the observed poor performance. 
    * Due to this there is often a tradeoff between the bias and variance contributions to the estimation error
        * "typically variance is reduced through smoothing via a combining of the influences of the samples that are nearby in the input space, this will however introduce bias as details of the regression function will be lost"
    * the bias component refers to the accuracy of a model on the data 
    * the variance component measures the amount of variation a model exhibits with regard to changes in the input data
* The performance of neural networks on difficult machine learning tasks is limited by the high dimension of the input space. Due to this solving these problems require "extrapolation rather than interpolation and nonparametric schemes yield essentially unpredictable results when asked to extrapolate."
* They conclude that learning complex tasks requires carefully designed biases to be apriori introduced into the model architecture
* They argue that some of these biases can be achieved through proper data representations.