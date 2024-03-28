---
layout: post
title: DPO
description: A short peek to the jouney of DPO
tags: LLM, DPO
---

This blog is trying to walk through the DPO paper and add all the basic concept


### Short history of RLHF

![](/assets/img/2024-02-26-RLHF-PPO-part2-img1.jpg)

The process begins with sampling from the environment, followed by the application of GAE for improved advantage approximation.

In this context, we consider human interaction as the “environment”. At each timestep, t, the
agent (i.e., the AI assistant) receives a state st from the environment (i.e., the dialogue history), which
consists of all the dialogue text up to this point, both by the assistant and the human. Then, based on
its policy π, the agent’s action at is to generate the next token. The environment returns a reward
r(st, at), which is calculated from a reward function r trained from human preference data. The
agent then transitions to the next state st+1, which includes the next dialogue history. The aim of RL
is to find an optimal behavior strategy for the agent to maximize the cumulative reward (i.e., return)
over a trajectory τ = {s1, a1, . . . , sT , aT }. One kind of return is finite-horizon undiscounted return
which is simply the sum of rewards accumulated within a fixed number of
steps. Another one is the infinite-horizon discounted return R(τ ) = P∞
account all rewards obtained by the agent throughout its entire trajectory with a discount factor
