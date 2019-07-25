# Summary of [Competing in the Obstacle Tower Challenge](https://blog.aqnichol.com/2019/07/24/competing-in-the-obstacle-tower-challenge/) by unixpickle

## Background
Solving a complex video game from pixel like Montezuma revenge but in 3D with controllable camera point of view.

## Take home message
* Use demonstration in a clever way

## Methods
### Starting point
Start with **primitives** that inject little information into the model (to be able to generalize):
* PPO on tiny observations (5x5 images)
* Open-loop action distribution with evolutionary algo.
* Always compare to random agent

### Problem with exploration
* Methods like [Curiosity-driven Exploration](https://arxiv.org/pdf/1705.05363.pdf) or [Go-Explore](https://arxiv.org/pdf/1901.10995.pdf)
are good for simple observation spaces but not for complex one: for example if you control the point of view of the camera, 
the same situation can look totally different and different situations can look alike. 
* Evolutionary algos (explore in parameter space instead of algo space) but use a lot of compute. 
* **Human demonstrations**: behavior cloning (early stopping to avoid overfitting) and then fine-tuning with PPO (*Can we finetune it with a RL aglo that learns a value function? Should we pretrain the value function on the demo?*)

### Agent memory problem
* RRN do not remember what you want them to and require a lot of samples.
* Simple representation that you can stack for a large number of timesteps (50) like (action, reward, some binary variable).
That can then be extended with a classifier's outputs, like "there is a door and a box on the screen" etc. 

### Agent policy forgetting
The entropy bonus that encourages random actions tends to destroy parts of the agent's pretrained behavior that do not yield noticeable rewards right away. 
* Should use [Prierarchy](https://blog.aqnichol.com/2019/04/03/prierarchy-implicit-hierarchies/) bonus instead of entropy

### Other tricks
* CNN architecture from the [IMPALA paper](https://arxiv.org/abs/1802.01561) that generalizes better
* [Fixup initialization](https://arxiv.org/abs/1901.09321) (instead of batch norm) to train deep nets
* [MixMatch](https://arxiv.org/abs/1905.02249) to train the classifier with little labels.
* For behavioral cloning used classic image data augmentation. And mirrored demonstration and actions to get two demonstrations out of one (straight and mirror)