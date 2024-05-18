# Reinforcement Learning for Cost Aware A/B testing Problem with Bandit-Model

## Problem Summary
The challenge focuses on a cost-aware A/B testing problem where multiple treatment options are available, and subjects are assigned to these treatments to evaluate their effectiveness. The uniqueness of the problem lies in minimizing the costs associated with assigning subjects to less effective treatments as their effectiveness becomes apparent. This is achieved by dynamically adjusting the assignment of subjects based on ongoing observations of treatment effectiveness.

## Problem and Task

**Problem Statement**: 

Formally, consider an experiment with $k$ treatment options $\{T_1, \ldots, T_k\}$ (no need to explicitly differentiate between treatment and control in a traditional sense, one of these options could be a control condition). Each of the $k$ treatments has a true underlying treatment effect $\{TE_1, \ldots, TE_k\}$, which is unknown to the experimenter before the experiment is conducted. For an arbitrary subject $i$ that is assigned to a treatment $j$, the realized treatment effect $TE_{ij}$ is a random draw from the normal distribution surrounding the true treatment effect with unknown variance, i.e., $TE_{ij} \sim N(TE_j, \sigma^2_j)$. There are $N$ subjects available in total, who can be assigned to the different treatment groups. The goal of the experimenter is twofold: (1) the experimenter wants to understand the effectiveness of each treatment option (this is why the experiment is conducted in the first place); (2) at the same time, the experimenter wants to be cost-aware in treatment assignment and try to avoid incurring too much costs.

## Reinforcement Learning Formulation
- Agent: The decision maker who allocates subjects to different treatment groups
- Environment: The agent will interact with the environment that consists of treatment outcomes, which include unknown true treatment effects.
- States: The accumulated observation and outcomes from historical assignment.
- Actions: The agenet's decision in each trails of how many and which subjects to assign to each treatment group
- Rewards: Positive rewards for allocations that lead to higher observed treatment effects, negative rewards for allocations that lead to lower ones.
- Objective: Maximize the cumulative reward and consider the statistical comparison

## Solutions 
1. Epsilon-Greedy with t-test Selection: Utilizes an epsilon-greedy approach for exploration and exploitation, adjusting action values based on the standard error of the mean to prioritize treatments with higher confidence in their effectiveness. Treatments are periodically evaluated and potentially eliminated based on statistical comparison using a t-test.

2. Epsilon-Greedy with Mann-Whitney U Test Selection: Similar to the first approach but uses the Mann-Whitney U test for arm elimination, making it suitable for non-normal reward distributions and providing robustness against skewed data.

3. UCB with Mann-Whitney U Test Selection: Replaces epsilon-greedy with Upper Confidence Bound (UCB) to strategically balance exploration and exploitation, adjusting the level of exploration through a tunable parameter.

## Implementation and Evaluation
Each method is implemented in a simulation environment where:

1. Treatment effects are predefined.
2. Subject responses are generated based on these effects.
3. The performance of each method is evaluated based on its effectiveness in optimizing treatment assignment and minimizing unnecessary costs.

The methods are compared to determine which offers the best trade-off between accurate treatment evaluation and cost efficiency in a dynamic assignment scenario.

<img width="471" alt="Screenshot 2024-05-16 at 4 36 50 PM" src="https://github.com/YenChenHsu/Reinforcement-Learning-with-Bandit-Model-/assets/57134574/a2ae3081-6014-4d5e-8cc8-fdd5eca2c90b">

