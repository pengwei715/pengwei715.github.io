---
layout: post
title: RLHF-PPO-part2
description: learning how to use PPO to do RLHF with phi2 model
tags: LLM, PPO, RLHF
---

This blog is the second part of the RLHF-PPO

### TRPO

- Trust region policy optimization enforces KL divergence constraint on the policy update
- It's doing off-policy RL. There are two policies. one is used for collecting trajectories. The othere one is used for optimization.
- Importance smpling is the objective function.
- Want to make sure the policy update is not too big. using the KL-divergence to measure the difference of two distribution. 


### PPO
-Introduce the clip function make sure the probability ratio between old and new policies are around 1.
-It takes the min between the origianl value from TRPO and the clip function.


### Goal of the RLHF

- Use iguazio to run the pipeline
- Find some bench mark dataset to make the comparison before and after RLHF
- Genaralize the function into the mlrun function hub


