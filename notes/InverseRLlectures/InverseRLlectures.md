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

index <img src="/notes/InverseRLlectures/tex/77a3b857d53fb44e33b53e4c8b68351a.svg?invert_in_darkmode&sanitize=true" align=middle width=5.663225699999989pt height=21.68300969999999pt/> is generalization on different MDP (or same MDP with different initial states)

#### Resolves
* access to <img src="/notes/InverseRLlectures/tex/b1384136386b001cacf877cd93c98628.svg?invert_in_darkmode&sanitize=true" align=middle width=16.69528244999999pt height=22.63846199999998pt/> by estimating it from trajectories
* ambiguity with structured prediction <img src="/notes/InverseRLlectures/tex/f29e60570324aebbca43573a46ec78c8.svg?invert_in_darkmode&sanitize=true" align=middle width=62.001682049999985pt height=24.65753399999998pt/>= number of states in which <img src="/notes/InverseRLlectures/tex/b1384136386b001cacf877cd93c98628.svg?invert_in_darkmode&sanitize=true" align=middle width=16.69528244999999pt height=22.63846199999998pt/> was observed and in which
<img src="/notes/InverseRLlectures/tex/f30fdded685c83b0e7b446aa9c9aa120.svg?invert_in_darkmode&sanitize=true" align=middle width=9.96010619999999pt height=14.15524440000002pt/> and <img src="/notes/InverseRLlectures/tex/b1384136386b001cacf877cd93c98628.svg?invert_in_darkmode&sanitize=true" align=middle width=16.69528244999999pt height=22.63846199999998pt/> disagree
* expert suboptimality: use of slack variable <img src="/notes/InverseRLlectures/tex/85e60dfc14844168fd12baa5bfd2517d.svg?invert_in_darkmode&sanitize=true" align=middle width=7.94809454999999pt height=22.831056599999986pt/>

#### Remaining challenges
Very large number of constraints: use subgradients methods or constraint generation

### Feature matching
<img src="feature_matching.png" alt="feature_matching.png" width="350"/> 

#### Apprenticeship learning [Abbeel & Ng, 2004](https://ai.stanford.edu/~ang/papers/icml04-apprentice.pdf)


Finds optimal policy and reward function. 
If suboptimal expert case:
* matches expert by stochastically mixing between the policies
* in practice if for any <img src="/notes/InverseRLlectures/tex/aa00beb6e7d6919d11e7d9d14416efdd.svg?invert_in_darkmode&sanitize=true" align=middle width=18.946040849999992pt height=22.63846199999998pt/> one of <img src="/notes/InverseRLlectures/tex/7d51fe947675789d633321fd5b787034.svg?invert_in_darkmode&sanitize=true" align=middle width=64.02417119999998pt height=14.15524440000002pt/> outperforms <img src="/notes/InverseRLlectures/tex/b1384136386b001cacf877cd93c98628.svg?invert_in_darkmode&sanitize=true" align=middle width=16.69528244999999pt height=22.63846199999998pt/> then pick one of them. 
* for k-dimensional feature space the user picks between k+1 policies.

**Problem:**
 at each algo step <img src="/notes/InverseRLlectures/tex/77a3b857d53fb44e33b53e4c8b68351a.svg?invert_in_darkmode&sanitize=true" align=middle width=5.663225699999989pt height=21.68300969999999pt/> we must guess the reward function
 <img src="apprentice_step1.png" width="450"/>
 
  and then **find the optimal control policy** <img src="/notes/InverseRLlectures/tex/fb7276301b30b0ad84054b52f14d0628.svg?invert_in_darkmode&sanitize=true" align=middle width=14.021211599999992pt height=14.15524440000002pt/>

Other solutions if suboptimal expert:
* Min-Max feature expectation matching
* Maximum-entropy feature expectation matching

### Reward function parameterizing the policy class
Recall :

 <img src="policy_param_by_r.png" width="400"/>

Assumes:

<img src="policy.png" width="350"/>

Then for any <img src="/notes/InverseRLlectures/tex/1e438235ef9ec72fc51ac5025516017c.svg?invert_in_darkmode&sanitize=true" align=middle width=12.60847334999999pt height=22.465723500000017pt/> and <img src="/notes/InverseRLlectures/tex/c745b9b57c145ec5577b82542b2df546.svg?invert_in_darkmode&sanitize=true" align=middle width=10.57650494999999pt height=14.15524440000002pt/> we can evaluate the likelihood state action-pairs along a trajectory with:
<img src="traj_proba.png" width="800"/>
