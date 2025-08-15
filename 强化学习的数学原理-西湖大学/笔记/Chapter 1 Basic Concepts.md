# Chapter 1 Basic Concepts

## 1.1 A grid world example

<img src="/Users/alannimoon/Library/Application Support/typora-user-images/截屏2025-08-08 19.54.34.png" alt="截屏2025-08-08 19.54.34" style="zoom:50%;" />

The ultimate goal of the agent is to find a “good” policy that enables it to reach the target cell when starting from any initial cell.

## 1.2 State and action

![截屏2025-08-08 19.58.38](/Users/alannimoon/Library/Application Support/typora-user-images/截屏2025-08-08 19.58.38.png)

The set of all the states is called the state space, denoted as S= {s1,...,s9}.

The set of all actions is called the action space, denoted as A= {a1,...,a5}. Diﬀerent states can have diﬀerent action spaces.

## 1.3 State transition

When taking an action, the agent may move from one state to another. Such a process is called state transition.

![截屏2025-08-08 20.00.31](/Users/alannimoon/Library/Application Support/typora-user-images/截屏2025-08-08 20.00.31.png)

Mathematically, the state transition process can be described by conditional probabilities. For example, for s1 and a2, the conditional probability distribution is

![截屏2025-08-08 21.01.24](/Users/alannimoon/Library/Application Support/typora-user-images/截屏2025-08-08 21.01.24.png)

Although it is intuitive, the tabular representation is only able to describe deterministic state transitions. In general, state transitions can be stochastic and must be described by conditional probability distributions.

## 1.4 Policy

A policy tells the agent which actions to take at every state.

![截屏2025-08-08 21.02.47](/Users/alannimoon/Library/Application Support/typora-user-images/截屏2025-08-08 21.02.47.png)

Mathematically, policies can be described by conditional probabilities. For example, the policy for s1 is

![截屏2025-08-08 21.04.48](/Users/alannimoon/Library/Application Support/typora-user-images/截屏2025-08-08 21.04.48.png)

The above policy is deterministic. Policies may be stochastic in general.

![截屏2025-08-09 19.40.09](/Users/alannimoon/Library/Application Support/typora-user-images/截屏2025-08-09 19.40.09.png)

Policies represented by conditional probabilities can be stored as tables.

![截屏2025-08-09 19.41.35](/Users/alannimoon/Library/Application Support/typora-user-images/截屏2025-08-09 19.41.35.png)

## 1.5 Reward

After executing an action at a state, the agent obtains a reward, denoted as r, as feedback from the environment. The reward is a function of the state s and action a. Hence, it is also denoted as r(s,a).

![截屏2025-08-09 19.43.18](/Users/alannimoon/Library/Application Support/typora-user-images/截屏2025-08-09 19.43.18.png)

![截屏2025-08-09 19.45.30](/Users/alannimoon/Library/Application Support/typora-user-images/截屏2025-08-09 19.45.30.png)

Although intuitive, the tabular representation is only able to describe deterministic reward processes. A more general approach is to use conditional probabilities p(r|s,a) to describe reward processes.

![截屏2025-08-09 19.46.06](/Users/alannimoon/Library/Application Support/typora-user-images/截屏2025-08-09 19.46.06.png)

## 1.6 Trajectories, returns, and episodes

![截屏2025-08-09 19.46.59](/Users/alannimoon/Library/Application Support/typora-user-images/截屏2025-08-09 19.46.59.png)

A trajectory is a state-action-reward chain.

![截屏2025-08-09 19.47.29](/Users/alannimoon/Library/Application Support/typora-user-images/截屏2025-08-09 19.47.29.png)

The return of this trajectory is defined as the sum of all the rewards collected along the trajectory:

![截屏2025-08-09 19.49.15](/Users/alannimoon/Library/Application Support/typora-user-images/截屏2025-08-09 19.49.15.png)

Returns can be used to evaluate policies. The return of the right policy is:

![截屏2025-08-09 19.50.13](/Users/alannimoon/Library/Application Support/typora-user-images/截屏2025-08-09 19.50.13.png)

The returns in (1.1) and (1.2) indicate that the left policy is better than the right one since its return is greater.

Return can also be defined for infinitely long trajectories.

![截屏2025-08-09 19.51.41](/Users/alannimoon/Library/Application Support/typora-user-images/截屏2025-08-09 19.51.41.png)

![截屏2025-08-09 19.51.58](/Users/alannimoon/Library/Application Support/typora-user-images/截屏2025-08-09 19.51.58.png)

which unfortunately diverges. Therefore, we must introduce the discounted return concept for infinitely long trajectories.

![截屏2025-08-09 19.53.48](/Users/alannimoon/Library/Application Support/typora-user-images/截屏2025-08-09 19.53.48.png)

where γ ∈(0,1) is called the discount rate. When γ ∈(0,1), the value of (1.3) can be calculated as

![截屏2025-08-09 19.54.17](/Users/alannimoon/Library/Application Support/typora-user-images/截屏2025-08-09 19.54.17.png)

The introduction of the discount rate is useful for the following reasons. First, it removes the stop criterion and allows for infinitely long trajectories. Second, the discount rate can be used to adjust the emphasis placed on near- or far-future rewards. In particular, if γ is close to 0, then the agent places more emphasis on rewards obtained in the near future. The resulting policy would be short-sighted. If γ is close to 1, then the agent places more emphasis on the far future rewards. The resulting policy is far-sighted and dares to take risks of obtaining negative rewards in the near future.

When interacting with the environment by following a policy, the agent may stop at some terminal states. The resulting trajectory is called an episode (or a trial). If the environment or policy is stochastic, we obtain diﬀerent episodes when starting from the same state. However, if everything is deterministic, we always obtain the same episode when starting from the same state.

Tasks with episodes are called episodic tasks. However, some tasks may have no terminal states, meaning that the process of interacting with the environment will never end. Such tasks are called continuing tasks. In fact, we can treat episodic and continuing tasks in a unified mathematical manner by converting episodic tasks to continuing ones. To do that, we need well define the process after the agent reaches the terminal state. We treat the terminal state as a normal state, we can simply set its action space to the same as the other states, and the agent may leave the state and come back again. 

## 1.7 Markov decision processes

The key ingredients of an MDP(Markov decision processes) are listed below.

![截屏2025-08-09 20.11.07](/Users/alannimoon/Library/Application Support/typora-user-images/截屏2025-08-09 20.11.07.png)

Here, p(s′|s,a) and p(r|s,a) for all (s,a) are called the model or dynamics. 

What is the diﬀerence between an MDP and an MP? The answer is that, once the policy in an MDP is fixed, the MDP degenerates into an MP.

![截屏2025-08-09 20.12.55](/Users/alannimoon/Library/Application Support/typora-user-images/截屏2025-08-09 20.12.55.png)

## 1.8 Summary

This chapter introduced the basic concepts that will be widely used in the remainder of the book. We used intuitive grid world examples to demonstrate these concepts and then formalized them in the framework of MDPs.