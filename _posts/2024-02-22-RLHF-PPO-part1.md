---
layout: post
title: RLHF-PPO-part1
description: learning how to use PPO to do RLHF with phi2 model
tags: LLM, PPO, RLHF
---

This blog record my learning process of how to use RLHF to do the alignment with phi-2 model on Iguazio platform

### Learning

#### Background knowledge of RL

- [A (Long) Peek into Reinforcement Learning](https://lilianweng.github.io/posts/2018-02-19-rl-overview/#key-concepts)
- [Policy Gradient Algorithms](https://lilianweng.github.io/posts/2018-04-08-policy-gradient/)
- [PPO paper](https://arxiv.org/abs/1707.06347)
- [Tech report of PPO from ByteDance and Fudan NLP](https://arxiv.org/abs/1707.06347)


#### Interesting take-aways

##### foundation knowledge
- Bellman Equations, The total value of the state is the immediate reward plust the discounted future values.

##### different type of RL

- Dynamic Programming is a type of Reinforcement learning. (The simplest type) we already know the distribution of actions from state i to state i+1. and the Reward of (s, a)
- Markov Decision Processes == Carpe diem. The future and the past are conditionally independent given the present. The current state encapsulates all the staticstics we need to decide the future.
- Monte-Carlo is different. The raw experience without modeling. And the observed mean is the exptected return. so It needs complete history of all states, actions, rewards. It seems like it enables the God view to know everything.




#### Policy Gradient Algorithms

