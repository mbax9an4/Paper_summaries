# [Spike-Train Level Backpropagation for Training Deep Recurrent Spiking Neural Networks](https://arxiv.org/abs/1908.06378)
## Authors: Wenrui Zhang, Peng Li

## Contributions
* This paper proposes a novel approach (operating at the spike train level) for performing backprop with recurrent spiking neural networks.
* The proposed algorithm (named ST-RSBP) computes the gradient of a rate-coded loss function defined over the output layer.
* ST-RSBP is shown to produce good results when used with layers that are either fully-connected, recurrent, or a mixture of the two.

## Motivation
* Addressing issues of existing backpropagation methods developed for training RSNNs (recurrent spiking neural networks): 
    * high complexity of unfolding in time
    * vanishing and exploding gradients
    * approximate differentiation of discontinuous spiking activities

* Biologically-inspired unsupervised training has limited capability in boosting performance of RSNNs. The authors argue that WTA and STDP learning can only be applied to the output layer which limits the adoption of deeper/more complex architectures. This statement is not true, see [Pfeiffer and Pfeil, 2018](https://www.frontiersin.org/articles/10.3389/fnins.2018.00774/full) for some examples of multi-layer STDP trained models.

* Most research on training SNNs is focused on feed-forward connections (which is natural as we want to ensure the method works as expected before further complicating the task). In many cases where recurrent SNNs are used the recurrent connections are either frozen or trained in an unsupervised manner using STDP. 

* Recurrent architectures could be an especially important area of research for spiking neural netowrks as such architectures are suited to processing temporal data.

## Why BPTT (Backpropagtion through time) is not suitable
1. recurrent connections have to be unfolded through time, after which the network can be viewed as a larger feed-forward network;
    * to capture the dynamics of the spiking neurons this network would have to be integrated through time
2. errors then have to be backpropagated (BP) through both time (due to spiking neurons) and space (due to unfolding connections);
    * BP would be applied across all layers using the stepsize defined for the simulation;
3. errors would have to be backpropagated over non-differentiable spike events.

## ST-RSBP properties
* can train arbitrary organizations of connections in RSNNs.
* does not incurr approximations resulted from altering and smoothing underlying spiking behaviours.
* does not require to unfold the network through time, which is a costly process. Instead BP is performed at each time point, leading to faster training times and avoiding vanishing/exploding gradients. 

## ST-RSBP 
### Advantages over extisting methods
* no unfolding of the recurrent connections is necessary
* more scalable than BPTT and less prone to vanishing/exploding gradients
* the backward learning step is conducted at the spike train level (so temporal characteristics of the spikes can be incorporated in learning) and not point by point in time
* temporal interactions between pre- and post- synaptic neurons are captured though Spike-train Level Post-synaptic Potentials (S-PSPs)

## Spike-train Level Post-synaptic Potentials (or S-PSP)
* S-PSPs capture the spike train level interactions between a pair of pre/post-synaptic neurons.
* The (normalized) S-PSP (defined as e_{ij}) from neuron j to neuron i is defined as: the accumulated contributions of the spikes produced by a pre-synaptic neuron j to the (normalized) post-synaptic potential of neuron i (right before spikes are produced in neuron i).
* S-PSPs are described as: the measure that enables the inclusion of temporal dynamics and recurrent connections of an RSNN (across all firing events at the spike train level) without needing to unfold the connections in time and backpropagate over individual time points.
* The total post-synaptic potential, or T-PSP is the sum of weighted S-PSPs over all pre-synaptic neurons of neuron i.
![T-PSP and the relationship between the output firing count of a post-synpatic neuron and its T-PSP.](diagrams/(1))

* The above diagram defines the relationship between the T-PSP (a_i) of a neuron i and its firing count o_i, via the firing threshold. 
* Relating the diagram to terminology of a traditional MLP, a_i and o_i can be interpreted as the pre-activation and post-activation values respectively, and g() acts as the activation function.

## ST-RSBP
* The T-PSP of a neuron l in a layer with index k+1 is defined as:
![Spike train activation and spike count of a neuron l in layer k+1.](diagrams/(2))
* In the above diagram T-PSP takes into account the feedforward connections (with weight w_{lj}^{k+1}) and the recurrent connections (weighted by w_{lp}^{k+1}) of neuron l.
* The loss to be minimized is a rate-coded MSE between the expected firing counts (as defined for the target label, in vector y) and the actual firing counts (vector o):
![Loss function.](diagrams/(3))
* Differentiating the loss produces:
![The back propagated error and the differentiation of activation terms.](diagrams/(4))
* Where the back propagated error at the output layer is given by:
![Loss function.](diagrams/(5))
* While at the hidden (feedforward) layers after the chain rule is applied the back propagated error is:
![Loss function.](diagrams/(6))
* And the hidden layers gradient for the recurrent connections is computed as:
![Loss function.](diagrams/(10))
* The weights are updated by:
![Weight update.](diagrams/(top page 5 delta w))

## Neuron model
* The authors mention that the neuron model is "based on the LIF model", this likely means that the SRM model is used, though this is not explicitly specified.

## Experiments
* Weights are initialized by sampling from a normal distribution over [-1,1].
* Exponential weight regularization is applied to prevent vanishing or exploding gradients.
* Lateral inhibition is applied on the output layer, to guide spiking behaviour towards the expected spike counts defined.
* Adam is used to optimize the weights during training.
* The desired output counts, firing thresholds, and learning rates are empirically tuned.
* A batch size of 1 is used.
* A simulation timestep of 1 is used.
* The accuracies reported represent the mean and best accuracy obtained over 5 repeats.
* _Datasets_: TI46-Alpha Speech Dataset, TI46-Digits Speech Dataset, N-Tdigits Neuromorphic Speech Dataset, Fashion MNIST Dataset
* _Results_: The accuracies reported outperform the accuracies of the models they have compared against. 

The code is available [online](https://github.com/AlexHoffman9/ST-RSBP). I am unsure if this is the official repo as no link is included in the paper.

There is a fair amount of overlap between this paper and the [Hybrid Macro/Micro Level Backpropagation for Training Deep Spiking Neural Networks](dsnn_backprop_macro_micro.md) paper. The main contribution of this paper is the consideration and derivation of the recurrent connections.