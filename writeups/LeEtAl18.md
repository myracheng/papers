# Hierarchical Imitation and Reinforcement Learning

Hoang M. Le, Nan Jiang, Alekh Agarwal, Miroslav Dudík, Yisong Yue, Hal Daumé III. [Hierarchical Imitation and Reinforcement Learning](https://arxiv.org/pdf/1803.00590.pdf) ICML 2018. 68 cites.


## abs
- hierarchical guidance: use hierarchical structure to integrate different types of experts

## intro
- imitation learning: watch and query expert. requires a large amount of demonstration data
- how to efifciently leverage feedback? use hierarchical structure
- high level experts feedback guides the low level learner


## background
imitation learning: passive (BC) (collect demonstrations beforehand, then find policy mimicking them) vs active (interactive)

hierarchical rl: existing `options framework`

combining rl + il: usually use IL as a pre-training step. but here, they consider feedback at multiple levels for a `hierarchical policy class`

## hierarchical formalism
`hi`: choosing subtask (subgoal)
`lo`: execute subtask (using primitive actions)
learner iteratively chooses a subgoal, executes it, and then picks a new one. agents choices depend on state s. 

hierarchical learning: learn `hi` policy (metacontroller) and subpolicy (MC for near, this is solved. are these policies dependent?)

hier. traj: (s1, g1, t1, s2, g2, t2,...) where t is a lo-level traj (s1, a1, ... s_h, a_h, s_{h+1}). so s_{h+1} coincides with s_{h+1} in the higher level trajectory

assume access to an expert (MC: how to build this expert for near?), which can do: 

- hier demo (expert executes the policy and return the resulting trajectory, so this is passive)
- labeling (providing a good next subgoal: provide labels with respect to the trajectories (current states inside the trajectories), so this is interactive) # QQ whats the diff?
- lo-level labeling/inspection (MC: so can tell you how good near will be? like neural heuristic
- labeling the trajectory-
- `inspect`: seeing whether the agent pass/fail. does not need to agree exactly at the low-level. often much less costly than labeling (assume o(1) MC not the case for near.)

## IL with hierarchical guidance (both levels are IL)
two ways:
1. only query low-level expert when needed
2. dont do low level when its not needed

h-BC: expert provides set of hierarchical demonstrations, which has lo- and hi-level trajectories. then, find subpolicies that correspond to those lo-level, and a meta-controller to correspond to the hi-level trajectories

hg-DAgger:
in dagger, expert provides correct actions + learners trajectories. naive implementatoin is to provide labels for the whole hierarchical trajectory. 
two hi-level query types: 
- inspect: verify whether subtask passes
- label: are we staying in the relevant part of the search space

theoretical analysis of savings in cost...
- most significant savings if horizons on each indiv level is shorter than the overall.
- reduce the cost of learning int o a constant factor

## with RL on low level
hi level expert provides decomposition
agents epxerience is added to the exp replay buffer if the subgoal agrees with the experts guidance - so if expert says we shouldnt explore that space, we dont include it.

predicates: basically a form of pseudo reward.

## experiments
- maze navigation, montezuma

## conclusion
- use weaker feedback like preference feedback, or bandit form of imitation learning
- learning the termination predicate (i.e. knowing whether subgoal achieved or not) - availaibility is assumed 
    - possible to simultaneously learn both?

basically we have access to knowing where is good and bad, which we dont really have in near.
- can we overcome this using MCMC or using heuristics at the high level?