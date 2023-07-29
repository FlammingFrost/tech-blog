---
title: 'Reinfroce Learning Note 1: Basic Notion'
seo_title: 'RL Note 1: Basic Notion'
summary: Summary shown on the post list.
description: A brief guide to post template. # not sure about the usage
slug: self-learn-log1
author: FlammingFrost
math: true # set to true to enable KaTeX rendering

draft: false # set to false to publish
date: 2023-07-28
lastmod: 2023-07-29 # both date and lastmod will show in the post's footer

feature_image:
feature_image_alt:

categories:
  - Reinforce Learning
tags:
  - RL
  - Log
series: 
  - Reinforce Self-learning Note

toc: true # set to true to enable a Table of Contents
related: true # set to true to enable Related Posts section
social_share: true # set to true to enable Social Sharing buttons
newsletter: false # set to true to enable Newsletter section, at the bottom of the page
disable_comments: false # set to true to disable comments for a specific post
---

Credit:

王树森 [深度强化学习网课](https://youtube/vmkRMvhCW5c)

[强化学习笔记 - 贝尔曼方程（Bellman Equation） - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/381821556?utm_id=0)


# Note 1: Basic Notion in Reinforce Learning

## Agent

A concept in reinforce learning that may OBSERVE the environment then TAKE ACTIONs. (Not strict definition).

## State $s$

State describes the information of agent. It could be its position, speed or any other conditions. It could also contain the information from the environment, but not necessary.

## Action $a$


In reinforce learning, agent takes actions to change its states and interact with the environment, aiming to achieve a higher reward. 

## Policy $\pi$

Policy describes how the agent decide its next (one) action $a$ after reaching state $s$.

Policy function $\pi$ can be viewed as a (conditional) possibility density function, with

**Def. Policy function**
$$
\pi(a|s) = Pr(A=a|S=s)
$$
When decision, agent always sample from the policy function (i.e by Gibbs sampling).

*The Policy is the learning objective of the trainingh of reinforce learning.*

## Reward $r$

Reward represents the objectives the model is about to obtain. It is a numerical value, and different actions can result in different reward. Reward is defined by the the designer, and it's also highly depend on the problem.

## State transition

How agent interact with the environment and manage to obtain higher reward is much like a process in statistics. It is a sequential structure where an old state transit to a new state one by one, and the action agent takes will affect such transition. We can formulate the transition by

**Def. State transition function**

$$
p(s'|s,a)=P(S'=s'|S=s,a=a)
$$

Similarly, here we again introduce the randomness by a possibility density function. However, we note that the randomness is NOT from the action, but from the environment itself, as the above function is conditional with $s$.

> Another point is that, this state transition function, detailing how the environment evolve, are supposed to be unknown by the players, namely agents.

## Agent-Environment Interaction

The interaction between Agent and Environment is recursive. A single iteration at time $t$ contain several basic steps: first the agent make a decision based on current state, $a_t\sim \pi(\cdot|s_t)$;  Then actions taken will alter the current state $s_t$ into next state $s_{t+1}$, $s_{t+1}\sim p(s'|s_t,a_t)$; meanwhile, the environment(game) will return reward $r_t$ as the feedback of agent's choice.

![The Process of Agent-Environment Interaction](D:\Data Field\Main Document_DDF\mdDocument\ResearchingNote\ReinforceLearning\绘图\Note1.1.png)

The whole process possesses two components of randomnessl. First randomness comes from Policy function $\pi$, and the second one originates from the state transition.

## Return & Discount return $U$

Return $U$ is defined as the sum of reward in the future, aka. culmulative reward.

$$
U_t = R_t + R_{t+1}+R_{t+2}+\cdots\qquad \text{Start from index }t
$$

> At time $t$, the importance of reward $r_s$ in future should not be equal , intuitively the reward in far futurn is full of uncertainty. Therefore, a common stategy is to reweight the reward while calculation return.

Discount return use exponential weighting to balance the uncertainty in future reward.

**Def. Discount return**
$$
U_t = R_t + \gamma R_{t+1} + \gamma^2R_{t+2}+\gamma^3R_{t+3}+\cdots
$$

where $\gamma$ is called discount rate, set as a hyper-parameter.

## Value Function $Q(s,a)$

As defined in previous section, given $s_t,a_t$, $U_t$ is a random variable depending on future actions $\{A_k\}$and states  $\{S_k\}, k = t,t+1,t+2,\cdots$. To evaluate the value of an action $a$ under policy $\pi$(because $U_t$ involves future decision), we take the expectation of rv. $U_t$:

**Def. Action-value function**
$$
Q_{\pi}(s_t,a_t)=\mathbb{E}[U_t|S_t=s_t,A_t=a_t]
$$
To free from the constrain of policy $\pi$, we find the best value among possible policies. The optimal value function $Q^*$ specifies the best possible performance. Agent can evaluate the value of an action base on OVF:

**Def. Optimal action-value function**
$$
Q^*(s_t,a_t)=\max\limits_{\pi} Q_{\pi}(s_t,a_t)
$$


Similarly, value function can estimate the situation in current state, here we take the expectation of action-value function with respect to action $a$.

**Def. State-value function**
$$
\begin{aligned}
V_\pi(s_t)=&\mathbb{E}_A[Q_\pi(s_t,A)]\\
=&\Sigma_a Q_\pi(s_t,A)\cdot \pi(a|s_t)\qquad&\text{(discrete)}\\
=&\int_a Q_\pi(s_t,A)\cdot \pi(a|s_t)da\qquad&\text{(continous)}
\end{aligned}
$$

### Understanding of Value function

- Generally, value function can evaluate how good is the Action/State/Policy.
- $Q_\pi(s,a)$ caluculate the expect return of an agent picking action $a$ while in state $s$, under policy $\pi$.
- Optimal action-value function evaluates the value of an action. Independent of policy.
- State-value function evaluates the "value" of a state. Under a specific policy.
- $\mathbb{E}_S[V\_{\pi}(S)]$ can be use to evaluate the performance of poilicy $ \pi $



## Two modes of Reinforce Learning

1. Policy-based Learning

   The AI learn the policy function $\pi$. When inferrence, model do random sampling $a\sim \pi(\cdot|s_t)$.

2. Value-based Learning

   The AI learn the optimal action-value function $Q^*$. The model then choose the action maximizing $Q^*$.



## Bellman Equation

> Bellman Equation is a tool for solving optimal value problem. There are other techniques can be used to tackle optimal control problem in deterministic setting. However, the **Bellman Equation** is often the most convenient method of solving stochastic optimal contreol problem, namely markov decision process(MDP).
>
> Bellman Equation is the basis of iterative reinforce learning.

### Markov Decision Process

Markov Decision Process is an nondeterministic modol containing 4 set of parameters $(S,A,P,R)$, together with discount $\gamma$.

| Notaion | Meaning                                     |
| ------- | ------------------------------------------- |
| $S$     | the set of states                           |
| $A$     | the set of action                           |
| $P$     | the state transition (possibility) function |
| $R$     | the return function                         |

- Start from initial state $s_0$, take action $a_0$, obtain reward $t_0$, then enter next state $s_1$, take another action $a_1$, ..., enter state $s_i$, take action $a_i$, obtain reward $t_i$, then enter next state $s_{i+1}$. Until final state $s_{terminal}$.

## Bellman Equation

Bellman Equation define state-value function, with policy function $\pi$.

In Bellman Equation, the state-value function is defined by
$$
V_\pi(s)=E_\pi[G_t|S_t=s]=E_\pi[\sum^\infty_{k=0}\gamma^kR_{t+k+1}|S_t=s]
$$
Noting that the definition of $G_t$ is the same nas discounted return $U_t$, the expectation over $\pi$  means expectation over all possible action $a$ taken by policy $\pi$. You find that this definition of state value function is identical to the definition given above.

Specially, we set the value of final state to zero, $V_\pi(s_{terminal})=0$.



Remenber that the problem is dicussed under markov process assumption, so the future after time $t$ is independent of information before $t$. Subsitute return with state-value function, assumming state transition function is known, then with discount $\gamma$,
$$
\begin{aligned}
V_\pi(s)=&E_\pi[\sum^\infty_{k=0}\gamma^kR_{t+k+1}|S=s_t]\\\\
=&E_\pi[R_{t+1}+\sum^\infty_{k=1}\gamma^kR_{t+k+1}|S=s_t]\\\\
=&E_\pi[R_{t+1}+\gamma E[\sum^\infty_{k=0}\gamma^kR_{t+k+1}|S=s_{t+1}]|S=s_t]\\\\
=&E_{s'\text{ from }\pi}[R_{t+1}+\gamma V_\pi(s')|s]
\end{aligned}
$$
or we can rewrite as
$$
\begin{aligned}
V_\pi(s)=&E_\pi[R_{t+1}+\gamma V_\pi(s_{t+1})|s_t=s]\\\\
=&
\left\\\{
\begin{array}{lr}
\sum_{s'}p(s'|s)\cdot [r_{s\rightarrow s'}+\gamma V_\pi(s')]\\\\
\int_{s'}f(s'|s)\cdot [r_{s\rightarrow s'}+\gamma V_\pi(s')]ds'\\\\
\end{array}
\right.
\end{aligned}
$$
This is so called Baellman equation. It calculates the state-value recursively.

