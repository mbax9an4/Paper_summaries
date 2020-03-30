Neural Network Ensembles, Cross Validation, and Active Learning 

Anders Krogh and Jesper Vedelsby 

* Learning of continuous valued functions using neural network ensembles (committees) can give improved accuracy, reliable estimation of the generalization error, and active learning.
* "A combination of the output of several networks (or other predictors) is only useful
if they disagree on some inputs."
* Main contribution is the derivation of the Ambiguity Decomposition for regression problems: "The simple and beautiful expression that relates the disagreement (called the ensemble ambiguity) and the generalization error is the basis for this paper, so we will derive it with no further delay."
* They position the decomposition in the context of the Bias-Variance decomposition. Thus the loss used to measure divergence is the quadratic error.
* The ensemble combination is a weighted arithmetic mean over the model predictions.
* They define the ambiguity or disagreement as: " the variance of the weighted ensemble around the weighed mean, and it measures the disagreement among the networks on input x."
* They the state the relationship between the ensemble error as a difference between the weighted sum of the model errors and a weighted sum of the model ambiguities. 
* "The beauty of this equation is that it separates the generalization error into a term that depends on the generalization errors of the individual networks and another
term that contain all correlations between the networks."
* AD expresses the tradeoff between bias and variance in the ensemble, but in a different way than the the common bias-variance relation in which the
averages are over possible training sets instead of ensemble averages. 
* " If the ensemble is strongly biased the ambiguity will be small, because the networks implement very similar functions and thus agree on inputs even outside the training set. Therefore the generalization error will be essentially equal to the weighted average of the generalization errors of the individual networks. If, on the other hand , there is a large variance , the ambiguity is high and in this case the generalization error will be smaller than the average generalization error."
* the generalization error of the ensemble is always smaller than the (weighted) average of the model errors, $E < \bar{E}$. In particular for uniform weights:
E \leq \frac{1}{N} \sum_{i=1}^N E_i

* "it is obvious that increasing the ambiguity (while not increasing individual generalization errors) will improve the overall generalization." So they then investigate how cross-validation can be used to encourage ensemble diversity. 
    * They train each model on a different fold, keeping one fold for testing
    * When holding out examples the generalization errors for the individual members of the ensemble, E(X, will increase, but the conjecture is that for a good choice of the size of the ensemble (N) and the test set size (K), the ambiguity will increase more and thus one will get a decrease in overall generalization error.