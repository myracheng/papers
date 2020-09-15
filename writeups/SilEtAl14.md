## Deterministic policy gradient algorithms

David Silver, Guy Lever, Nicolas Heess, Thomas Degris, Daan Wierstra, Martin Riedmiller. [Deterministic Policy Gradient Algorithms.](http://proceedings.mlr.press/v32/silver14.pdf) ICML 2014. 1554 cites.

dpg: expected gradient of action-value function.

### intro
policy gradient: policy is a parametric probability distribution P*a|s*, stochastic selection.
- adjust parameters \theta in direction of performance gradient
- not dependent on gradient of state distribution
- integrate over state and action space
https://lilianweng.github.io/lil-log/2018/04/08/policy-gradient-algorithms.html#what-is-policy-gradient

Instead, we consider deterministic: *a = \mu(s)* which is the limiting case of stochastic policy gradient.
- integrates only over state space, so requires less samples

stochastically choose actions (exploration) to learn about deterministic policy.

### algo
actor critic: adjust parameters of policy using policy gradient, and use action-value function Q^w(s,a) that is learned/estimated by critic to approximate Q^pi(s,a). w is parameter that minimizes error 

off-policy actor critic: estimate gradient from trajectories from a policy that is not pi_theta. Drops the term based on Q^pi(s,a)

improve policy by taking step in direction of gradient of Q. gradient of action value & gradient of policy

todo - understand derivation of policy gradient theorem [x](https://papers.nips.cc/paper/1713-policy-gradient-methods-for-reinforcement-learning-with-function-approximation.pdf)


# Policy Gradients - tbf

[lil blog](https://lilianweng.github.io/lil-log/2018/04/08/policy-gradient-algorithms.html#what-is-policy-gradient)

## DDPG