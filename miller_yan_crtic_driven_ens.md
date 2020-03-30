# [Critic Driven Ensemble Classification](https://ieeexplore.ieee.org/document/790663)

**Authors**: David Miller and Lian Yan

* The authors compare several methods of combining model predictions in a multi-class context.
* They include mention of using the normalized geometric mean to combine predictions that represent class probability estimates, showing how the KL divergence between two categorical distributions reduces to the cross entropy loss over the class estimates.
    * If we view the expert probabilities as priors, then we will choose the combined probabilities as the posteriors minimizing the average cross entropy cost