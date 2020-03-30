# [SpiLinC: Spiking Liquid-Ensemble Computing for Unsupervised Speech and Image Recognition](https://www.frontiersin.org/articles/10.3389/fnins.2018.00524/full)

**Authors**: Gopalakrishnan Srinivasan*, Priyadarshini Panda and Kaushik Roy, 2018

* They propose using an ensemble to combine learning from two data types that describe the same problem: recognizing digits from images and from speech.
* They use a liquid spiking model
    * input layer sparsely connected by plastic synapses to a liquid containing excitatory and inhibitory neurons recurrently interlinked in sparse random manner
    * the ratio of excitatory neurons to inhibitory neurons is 4 to 1 as observed in cortical microcircuits
    * The non-linear spiking neuronal dynamics together with sparse recurrent connectivity triggers the liquid to produce diverse spiking patterns, referred to as liquid states, for inputs with disparate temporal characteristics. The state of the liquid at any given time is a high dimensional representation incorporating the input dynamics both at the current and preceding time instants. It is important to note that sparsity in synaptic connectivity is essential for a liquid to generate discernible states. 
    * we tag the excitatory neurons in the liquid with the classes of input patterns for which they spiked at a higher rate during the training phase
* To combine: the average firing rate of each class is computed by taking the arithmetic mean over the spike counts recorded for all neurons associated with the same class. The class with the highest score is predicted.
* The unsupervised STDP algorithm proposed by [Diehl et.al](https://www.frontiersin.org/articles/10.3389/fncom.2015.00099/full) is used for training