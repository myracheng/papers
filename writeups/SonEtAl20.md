# A General Large Neighborhood Search Framework for Solving Integer Linear Programs

Jialin Song, Ravi Lanka, Yisong Yue, Bistra Dilkina. [A General Large Neighborhood Search Framework for Solving Integer Linear Programs](https://arxiv.org/abs/2004.00422) NeurIPS 2020. 0 cites.

## abstract
- solve integer programs using large neighborhood search (LNS)
    - iteratively choose subset of variables to optimize, fix the rest
        - even randomly doing this works better than not QQ why??

## introduction +related work
- typical approach for combinatorial problems and learning good params for their algorithms is ``learning to search``: take existing template, replace hard-coded part with parametrizable version
    - e.g. branch and bound to pick. often trained using reinforcement/imitation learning
    - other approaches: optimize parameters for each problem (`algorithm configuration`), learninng to predict subtructures (but this makes a lot of assumptions about structure, which we dont need)

## algo
decomposition-based LNS that operates on generic ILP
- neighborhood fn N(s) is candidate solutions set. defined implicitly through _destroy_ and _repair_ methods. --> neighborhood is large since exponential options
- LNS has been used as local search heuristic, requires access to the underlying solver QQ what does this mean? to train it?
- decompose into disjoint subsets. pick subset and optimize those, hold X\X_i fixed. 

## learning a decomposition
state is a vector for assignment of variables (i.e. existing solution)
action is a decomposition
reward `r(s,a) = J(s) - J(s_n-1)`
- reinforcement learning using REINFORCE to maximize reward. estimate gradient by sampling trajectories
- imitation learning: sample random decompositions, take the best ones as demonstrations. use behavior cloning to treat this as a supervised learning problem. MC: for prog context with supervised learning, we can directly evaluate it? so we dont need to use RL

### featurization
- problems defined explicitly over graphs, like vertex cover --> use adjacency matrix of graph as feature input
QQ uhh what is this section for?
- a: how to construct matrices to put into the learning model. so i guess this is just for the learning part

## empirical results
- for RL, sample 5 trajectories. for IL, sample 5 random and use the best one as decomposition
- hyperparameter: number of subsets to divide the variables into, and how long to solve each problem
- all variants significantly outperform Gurobi, much faster
- imitation learning based are better than random and RL

## misc 
- `backdoor variables`: set of variables that simplifies the problem into a tractable one
- [Gurobi](https://www.gurobi.com/): state-of-the-art solver
