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

### Steps:

- The reward model can be a transformer-based languge model with the last unembedding layer removed and add an additional linear layer to the final transfomer layer.
- State in the RL: 

at time t, the state is all the conversation text up to this point, both by the model and the human. Based on its policy, the agent's action a is to generate the next token. The reward is a value with respect of state and action. this is calculated froma reward function. 
- Policy Gradient Methods. 

optimize the policy of the agent (mapping fo states to actions). Not learning the value function. Improve the policy using the gradient ascent algorithm. The native policy Gradient Method is using monte carlo sampling with actual return. it has bigger variance issue. So a common strategy is to use advantage function estimates return. It shows how much better it's to tkae a specific action a at state s, compared to the average quality of actions at that state under the same policy. it's just the action-value - state-value
- Generalized Advantage Estimation
instead of only 1 step look ahead as temporal difference. we use k-steps TD. So there will be some trade-off between bias and variance. if k is small, high bias, low variance. if k is large, low bias, high variance. To banlance that. GAE defineds a exponential moving average with weights.

- Need two models to train during the PPO training:
1. Critic: this is the value function
2. Actor: this is the policy function

- Alg (this is the implementation of the huggingface's trl lib)

$$
\begin{align*}
1. & \text{ \textbf{Input:}} \text{ initial policy parameters } \theta_0, \text{ initial value function parameters } \phi_0. \\
2. & \text{ \textbf{for} } n = 0, 1, 2, \ldots \text{ \textbf{do}} \\
& \quad a. \text{ Collect a set of trajectories } D_n = \{\tau_i\} \text{ by executing policy } \pi(\theta_n) \text{ within the environment.} \\
& \quad b. \text{ Compute rewards-to-go } \hat{R}_t. \\
& \quad c. \text{ Compute advantage estimates, } \hat{A}_t \text{ (using any advantage estimation method) based on the current value function } V_{\phi_n}. \\
& \quad d. \text{ Update the policy by maximizing the PPO-penalty/clip objective:} \\
& \qquad \theta_{n+1} = \arg \max_\theta L_{\text{ppo-clip}}(\theta_n). \\
& \quad e. \text{ Update the value function by regression on mean-squared error:} \\
& \qquad \phi_{n+1} = \arg \min_\phi L_{\text{critic}}(\phi_n). \\
3. & \text{ \textbf{end for}}
\end{align*}
$$




### Pain point

- The PPO need a ref model, reward model, orignal model to work together for the alignment training. we only have 5 T4 GPUs to use. it will be super chanllege. 
