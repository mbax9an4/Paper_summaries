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