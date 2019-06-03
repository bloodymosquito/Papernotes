# Summary of [Learning Latent Plans from Play](https://arxiv.org/pdf/1903.01973.pdf) by Lynch et al.

## Idea
They use play data (an operator is teleoperating a robotic arm for 3h with no precise goal) to do self-supervised learning
and learn the sequence of actions that get the agent from a given state <img src="/notes/LatentPlansFromPlay/tex/4fa3ac8fe93c68be3fe7ab53bdeb2efa.svg?invert_in_darkmode&sanitize=true" align=middle width=12.35637809999999pt height=14.15524440000002pt/> to a goal state <img src="/notes/LatentPlansFromPlay/tex/2fe2e7ed4121dbe038f264917011be6d.svg?invert_in_darkmode&sanitize=true" align=middle width=14.53144934999999pt height=14.15524440000002pt/>. 
Then they can do multi-task control by providing the current state of the robot and the desired goal state. 

They explicitly learn a latent representation of the possible plans (sequence of actions) that go from <img src="/notes/LatentPlansFromPlay/tex/4fa3ac8fe93c68be3fe7ab53bdeb2efa.svg?invert_in_darkmode&sanitize=true" align=middle width=12.35637809999999pt height=14.15524440000002pt/> to <img src="/notes/LatentPlansFromPlay/tex/2fe2e7ed4121dbe038f264917011be6d.svg?invert_in_darkmode&sanitize=true" align=middle width=14.53144934999999pt height=14.15524440000002pt/>.
By doing this they can handle the multi-modality present in each task (many ways to reach the same goal).  

## Specifics
The sequence encoder that learns the latent plans representation is a bi-directional RNN. The policy is a RNN. 

## Limitations
"Like other methods training goal-conditionned policies, we assume that tasks important to a user can be described
using a single goal state". Not really adapted for adversarial tasks where the agent does have control over the whole
state and must react/re-plan depending on the adversaries actions. 

## Relevance to project
Our "plans" are influenced by the other agents and change dynamically. We cannot ensure that our plan stays constant over
a trajectory.

We might be more interested in something like Play-GCBC that is less effective but where there is no explicit latent plan
inference.
## Overview
### Architecture 
#### Training
<figure>
 <img src="training.PNG" width="800"/> 
</figure>

#### Evaluating
 <img src="evaluating.PNG" width="800"/>
 
### Results
#### Asymptotic Performance:
 <img src="asymptotic_perf.PNG" width="800"/>
 
#### Robustness
 <img src="robustness.PNG" width="800"/>

#### Latent Plans
 <img src="latent_plans.PNG" width="800"/>