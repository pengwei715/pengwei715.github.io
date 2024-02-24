---
layout: post
title: RLHF-PPO-part1
description: learning how to use PPO to do RLHF with phi2 model
tags: LLM, PPO, RLHF
---

This blog record my learning process of how to use RLHF to do the alignment with phi-2 model on Iguazio platform.

### Learning

#### Background knowledge of RL

- [A (Long) Peek into Reinforcement Learning](https://lilianweng.github.io/posts/2018-02-19-rl-overview/#key-concepts)
- [Policy Gradient Algorithms](https://lilianweng.github.io/posts/2018-04-08-policy-gradient/)
- [PPO paper](https://arxiv.org/abs/1707.06347)
- [Tech report of PPO from ByteDance and Fudan NLP](https://arxiv.org/abs/1707.06347)


#### Interesting take-aways

- Dynamic Programming is a type of Reinforcement learning. (The simplest type) we already know the distribution of actions from state i to state i+1. and the Reward of (s, a)
- Bellman Equations, The total value of the state is the immediate reward plust the discounted future values.
- Markov Decision Processes == Carpe diem. The future and the past are conditionally independent given the present. The current state encapsulates all the staticstics we need to decide the future. This is a very very strong assumption.
- Monte-Carlo is different. The raw experience without modeling. And the observed mean is the exptected return. so It needs complete history of all states, actions, rewards. It seems like it enables the God view to know everything.


- Temporal-Difference Learning. Unlike Monte-Carlo, we don't need the whole episodes. 
1. Bootstrapping. only use the exsiting estimates. Don't need exact values like Mente-Carlo
2. TD target: update the value function towards an estimated target with hyperparameter a. 
3. SARSA: on-policy TD control, for each iteration, find the action a that can max Q. For MC, we have all different episodes to use. for this one, only one. 

On-policy learning: "learn on the job"

Off-policy learning: "look over someone's shoulder" RLHF ??

Greedy in the limit with infinite exploration(GLIE)

GLIE Monte-Carlo Control

All state-action pairs are explored infinitely many times.


model-free means know nothing or little thing about MDP


#### Policy Gradient Algorithms

