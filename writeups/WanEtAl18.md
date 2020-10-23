# MetaLearning MCMC Proposals

Tongzhou Wang, Yi Wu, David A. Moore, Stuart J. Russell. [MetaLearning MCMC Proposals.](https://arxiv.org/pdf/1708.06040.pdf) NeurIPS 2018. 12 cites.

## abstract
meta-learning approach for mcmc proposal distribution. parametrize proposal as NN, fast approximation to block gibbs conditionals

## introduction
probabilistic programming: models as sample generating programs

require manually designed proposal distributions

`single-site gibbs sampling`: TODO, slow sampling
    - naive MCMC algorithm: generate MC of samples, each of which is correlated with nearby samples. special case of MH algo: the next sample is a vector, so we sample each component from the distribution conditioned on all other components sampled so far. so for index j of i+1, we condition on i+1(1:j) and i(j+1:n). by repeating this, we approximate the joint distirbution of all variables
    - gibbs sampling is used for inference, e.g. determining best value of a parameter (so its effectively a posterior distribution based on the observed data). then like a MAP estimate, we just choose the value that occurs the most. or we can take the expected value
    - supervised learning: fix the valuesu of variables whose values are known

`block proposals`: update multiple variables together
    - but hard to compute exact gibbs proposals for large blocks

they design a proposal (distrib) that works on any model with similar local structure, which single site Gibbs (ssg) does not achieve.
    - this is reusable across different models
    - this is effective for fast mixing (time for MC to achieve steady state distrib)
    - learn approximate block-Gibbs proposals

1. generate diff instantiations of a motif by randomizing parameters
2. train neural proposal clos eto the true gibbs conditions for all instantiations

meta learning: generate many training environments, train a learning agent to succeed in all of them. *generalizable* MCMC proposals.

apply this to compare it to Gibbs sampling. 

basically genreating an approximate posterior.
## related work
- VAEs: train inference network jointly. 
- model-specific MCMC proposals w/ machine learning techniques

## section 3
use nn to approximate gibbs proposal distrib for recurring structural motif.

`mixture density networks`, min the KL divergence b/w true posterior conditional and the proposal by sampling instantiations of the motif. proposals are accepted/rejected based on MH rule, so we maintain the correct \pi.

### 3.1
directed models: graph where nodes are variables, and we have set of factors specifiying joint prob distrib p(V). factors specify conditional probability distributions of each variable given its parents. 

given set of observed evidence variables, inference attempts to sample from conditional distribution on the rest of them. take advantage of structural motifs (grids, rings, chains)

we want to train an NN that makes expert proposal on structural motif. and then this proposal can be applied to diff models. proposal network maps vals of conditional variables and local parameters to a distribution over the proposed variables.

### 3.2
sturctural motifs: determine shape of network inputs and outputs. structural motifs are arbitrary subgraphs. we want motifs that represent conditional structure between block proposed variables B and conditioning variables C.

structural motif is a graph with nodes partitioned into two sets B and C.

natural choice for C is the Markov blanket (the variables that are not useless). might chooose a subset. 

our goal is to learn block proposal q(B_i|C_i, factors) such that its an element of the support of C (?? QQ equation 1), q(B_i, c_i, factors) \approx p(B_i | C_i = c_i)
    - if complex structures, the conditionals  p(B_i | C_i = c_i) can be quite different for diff instantiations. 

- use common structures

### 3.3
mixture density networks: output parametrizes a mixture distribution, and in each mixture component, the variables are uncorrelated.

neural bloc proposal is q parametrized by an MDN with weights theta.

### 3.4 
loss function: KL divergence
to train, we generate a set of random instantiations and optimize the loss function over all of them. our goal is to minimize the overall loss

build a library of neural block proposals trianed on common motifs

## Experiments
on grids, mixtures, and chains which are common structural motifs.

to design the proposal, use small MDNs, and choose a distribution to generate parameters that maximize the space covered.

## conclusion
meta learning gneeralizable to approximate block gibbs proposals. can be applied to novel models given a common set of structural motifs

qq connections to program syntehsis? or apply it to learning programs?


# [Program Synthesis Lecture 5:  Inductive Synthesis with Stochastic Search.](https://people.csail.mit.edu/asolar/SynthesisCourse/Lecture5.htm)

stationary distirbution \pi_x. 
probability matrix K. create K so that \pi is high for good programs, low for bad programs

Metropolis Hastings algorithm: start with J(x, y) which is a Markov matrix that is the proposal distribution. 

acceptance ratio: (\pi(y) * J(y,x))/(\pi x * J(x,y))

## using MH for program snthesis: 
silly example would be J is uniform, \pi is 1 for correct program. but \pi cannot be zero for any x, so we need it to be some value > 0.
we need pi that allows us to tell if program is getting closer to being corect. and J gives priority to behaviors that are similar (so gradual/gradient-esque search)

with probabiliy p_s, swap two rando minstructions.
p_u, pick one instruction and replace it with a no_op

stationary distribution has correctness component and performance component.

creates almost disjoint clusters

*describe proposal distribution J using probabilitistic process to transition beween programs.* QQ what does this look like?



so we are trying to define J and \pi.
J(T,R)

run candidate program on test inputs and compute distance between outputs. 

define stationary ddistribution in terms of a cost function, e.g. # of examples that it got wrong (want to capture almost ocrrect)

so question becomes how do we learn J and define \pi?