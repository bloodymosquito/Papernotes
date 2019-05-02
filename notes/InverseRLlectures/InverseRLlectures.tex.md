# Summary of [Inverse Reinforcement Learning](https://people.eecs.berkeley.edu/~pabbeel/cs287-fa12/slides/inverseRL.pdf) by Pieter Abbeel

## Background
* **Inverse RL**: Can we recover *R* ? 
* **Apprenticeship learning via inverse RL**: Can we then use this *R* to find a good policy?
* **Behavioral Cloning**: Can we directly learn the teacher's policy using supervised learning?  

## Three broad categories of formalizations
* Max margin
* Feature expectation matching
* Interpret reward function as parameterization of a policy

## Basic principle
Assume the expert is optimal and find a reward function which explains the expert behavior. i.e find *R** such that
<img src="BasicPrinciple.png" alt="Eq_basic_principle" width="400"/>

## Feature based reward function
<img src="feature_based.png" alt="Eq_basic_principle" width="600"/>

Then, finding *R** becomes:

<img src="feature_based_principle.png" alt="Eq_basic_principle" width="400"/> 

#### Challenges
* Estimate expert feature expectations (from trajectories for example)
* Reward function ambiguity: expert is optimal under an many different reward functions (*R**=0 is always a solution)
* Assumes that the expert is optimal (is even more a issue with limited reward function expressiveness)
* Computational: assumes we can enumerate all policies

### Complete max-margin formulation
<img src="complete_max_margin.png" alt="complete_max_margin.png" width="600"/> 

index $i$ is generalization on different MDP (or same MDP with different initial states)

#### Resolves
* access to $\pi^*$ by estimating it from trajectories
* ambiguity with structured prediction $m(\pi^*,\pi)$= number of states in which $\pi^*$ was observed and in which
$\pi$ and $\pi^*$ disagree
* expert suboptimality: use of slack variable $\xi$

#### Remaining challenges
Very large number of constraints: use subgradients methods or constraint generation

### Feature matching
<img src="feature_matching.png" alt="feature_matching.png" width="350"/> 

#### Apprenticeship learning [Abbeel & Ng, 2004](https://ai.stanford.edu/~ang/papers/icml04-apprentice.pdf)


Finds optimal policy and reward function. 
If suboptimal expert case:
* matches expert by stochastically mixing between the policies
* in practice if for any $w^*$ one of $\pi_0,\pi_1,\pi_2$ outperforms $\pi^*$ then pick one of them. 
* for k-dimensional feature space the user picks between k+1 policies.

**Problem:**
 at each algo step $i$ we must guess the reward function
 <img src="apprentice_step1.png" width="450"/>
 
  and then **find the optimal control policy** $\pi_i$

Other solutions if suboptimal expert:
* Min-Max feature expectation matching
* Maximum-entropy feature expectation matching

### Reward function parameterizing the policy class
Recall :

 <img src="policy_param_by_r.png" width="400"/>

Assumes:

<img src="policy.png" width="350"/>

Then for any $R$ and $\alpha$ we can evaluate the likelihood state action-pairs along a trajectory with:
<img src="traj_proba.png" width="800"/>
