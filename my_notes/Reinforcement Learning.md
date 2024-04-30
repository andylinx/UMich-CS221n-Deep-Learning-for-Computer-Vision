# Reinforcement Learning

an agent performs actions in environment, and receives rewards

goal: Learn how to take actions that maximize reward



**Stochasticity**: Rewards and state transitions may be random

**Credit assignment**: Reward $r_t$ may not directly depend on action $a_t$

**Nondifferentiable**: Can't backprop through the world

**Nonstationary**: What the agent experiences depends on how it acts



## Markov Decision Process (MDP)

Mathematical formalization of the RL problem: A tuple $(S,A,R,P,\gamma)$

$S$: Set of possible states

$A$: Set of possible actions

$R$: Distribution of reward given (state, action) pair

$P$: Transition probability: distribution over next state given (state, action)

$\gamma$: Discount factor (trade-off between future and present rewards) 



**Markov Property**: The current state completely characterizes the state of the world. Rewards and next states depend only on current state, not history.



Agent executes a policy $\pi$ giving distribution of actions conditioned on states.

**Goal**: Find best policy that maximizes cumulative discounted reward $\sum_t \gamma^tr_t$



![image-20240429140008257](C:\Users\13123\AppData\Roaming\Typora\typora-user-images\image-20240429140008257.png)



We will try to find the maximal expected sum of  rewards to reduce the randomness.



Value function $V^{\pi}(s)$: expected cumulative reward from following policy $\pi$ from state $s$

Q function $Q^{ \pi}(s,a)$ : expected cumulative reward from following policy $\pi$ from taking action $a$ in  state $s$



###### Bellman Equation

After taking action a in state s, we get reward r and move to a new state s'. After that, the max possible reward we can get is $\max_{a'} Q^*(s',a')$



**Idea**: find a function that satisfy Bellman equation then it must be optimal

start with a random Q, and use Bellman equation as an update rule.

![image-20240429143821850](C:\Users\13123\AppData\Roaming\Typora\typora-user-images\image-20240429143821850.png)

But if the state is large/infinite, we can't iterate them.

Approximate Q(s, a) with a neural network, use Bellman equation as loss function.

-> Deep q learning



### Policy Gradients

Train a network $\pi_{\theta}(a,s)$ that takes state as input, gives distribution over which action to take

###### Objective function: Expected future rewards when following policy $\pi_{\theta}$

Use gradient ascent -> play some tricks to make it differentiable



![image-20240429150706752](C:\Users\13123\AppData\Roaming\Typora\typora-user-images\image-20240429150706752.png)



#### Other approaches:

Actor-Critic

Model-Based

Imitation Learning

Inverse Reinforcement Learning

Adversarial Learning

...

Stochastic computation graphs

