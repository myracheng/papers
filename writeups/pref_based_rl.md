# Notes from Reading Group on Pref-Based RL
## Inverse Reinforcement Learning (Arora et al)

Use human behavior to learn policy, dont explicitly define reward, enables learning from demonstration
Learn a R from the observed state/action pairs
> RL seeks to learn the optimal behavior based on experiences ((s, a, r)) that include obtained rewards, IRL seeks to best explain the observed behavior by learning the corresponding reward function.

Reward function is more transferable than the specific policy for an agent

An MDP is a framework that the probability of moving into a state s is influenced by the chosen action, specifically, a transition function P_a(s, s’).

The observed agent is assumed to follow an optimal policy for the MDP

Value is the expected sum of rewards


### Problems:
- Many diff reward functions can explain it
- How to measure accuracy?
- measure the difference in values of the learned and true policies. Specifically, we may measure the error in inverse learning, called inverse learning error
- Learned behavior accuracy 
- Generalizability
- Depends on prior knowledge
- Curse of dimensionality of state space, sample complexity

### Approaches:
- Approximate the reward using input data
- Relies on selecting the right features to weight
- Learn a policy whose actions match the behavior

## Preference Based Reinforcement Learning (Wirth et al)
- Use prefs instead of reward fn
- Uses weak/strong preferences
- MDPP (Preference learning over trajectories (sets of s/a))
- However, satisfying this condition is typically not sufficient as the difference can be infinitesimal. Moreover, due to the stochasticity of the expert, the observed preferences can also contradict each other.
    So define it in terms of probability (eq 2)
- Each preference defines a loss function
    - Since losses can interfere with each other, assign different weights to them
- Want “maximizes the realization probability of undominated trajectories while not generating dominated trajectories”
- Define criteria to present the two trajectories to the expert
- Related work:
    - Advice based algorithm
    - Irl: TRAJECTORIES supplied by EXPERT
        - IRL approaches are not able to obtain new feedback for trajectories and, hence, can not improve upon the expert demonstrations
    - This is a dueling bandit problem where policies are arms
- Prefs based on indiv state or actions: require less expertise, but unclear how it helps long term optimality
- Challenge with trajectory prefs: algorithm needs to determine which states or actions are responsible for the encountered preferences, which is also known as the temporal credit assignment problem
- Many different approaches for utility function:
    - a linear utility function, we can define a loss function L which is given by the (weighted) sum of the pairwise disagreement loss L
        - Indicator loss: doesnt account for noise in preferences. So we want to use continuous loss functions
        - Sigmoid:  saturate the effect of a high utility differences
- Preference elicitation: if u want to do it online
- Other sections: Preference generation, Policy optimization, Modeling Transition Dynaimcs, Robotics Applications
- GAIL: desire an algorithm that tells us explicitly how to act by directly learning a policy https://arxiv.org/abs/1606.03476

## Human-in-the-loop Reward Papers
1. Arora and Doshi, “A Survey of Inverse Reinforcement Learning.”
2. Christiano et al., “Deep Reinforcement Learning from Human Preferences.”
    * Follow up: http://papers.nips.cc/paper/8025-reward-learning-from-human-preferences-and-demonstrations-in-atari.pdf
3. Reddy et al., “Learning Human Objectives by Evaluating Hypothetical Behavior.”
4. Sugiyama, Meguro,* and Minami, “Preference-Learning Based Inverse Reinforcement Learning for Dialog Control.”
5. Toyoda, Ogawa, and Haseyama, “Video Classification Based on User Preferences with Soft-Bag Multiple Instance Learning.”
6. Leike, Jan, et al. "Scalable agent alignment via reward modeling: a research direction." arXiv preprint arXiv:1811.07871 (2018).
7. Bıyık, Erdem, and Dorsa Sadigh. "Batch active preference-based learning of reward functions." arXiv preprint arXiv:1810.04303 (2018).
8. DPS https://arxiv.org/pdf/1908.01289.pdf

## Other notes
> In the work of Christiano et al., 2017, it is shown how learning a separate reward model using supervised learning lets us significantly reduce the amount of feedback required from a human teacher. They also present the first practical applications of using human feedback in the context of deep RL to solve tasks with a high dimensional observation space (https://arxiv.org/pdf/1811.12560.pdf)

> Christiano et al. (2017) propose to learn a reward function based on human preferences by comparing pairs of trajectory segments. The proposed method maintains a policy and an estimated reward function, approximated by deep neural networks. The networks are updated asynchronously with three processes iteratively: 1) produce trajectories with the current policy, and the policy is optimized with a traditional RL method, 2) select pairs of segments from trajectories, obtain human preferences, and, 3) optimize the reward function with supervised learning based on human preferences. Experiments show the proposed method can solve complex RL problems like Atari games and simulated robot locomotion


https://www.aaai.org/Papers/AAAI/2008/AAAI08-227.pdf
MaxEnt IRL
Imitation learning: is trying to do what an agent would do. 
IRL: match feature expectations

https://arxiv.org/pdf/1611.03852.pdf
Maxent irl == gan, special case of an EBM. The learned cost in MaxEnt IRL corresponds to the energy function, and is trained via maximum likelihood

> Bradley-Terry model (Bradley and Terry, 1952) for estimating score functions from pairwise preferences, and is the specialization of the Luce-Shephard choice rule (Luce, 2005; Shepard, 1957) to preferences over trajectory segments
