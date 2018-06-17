Our suit of custom games built for our paper

We used the PyGame-Learning-Environment to build these games. All the games are based on the codes from the game 'MonsterKong' from PLE. 

## Getting started

A `PLE` instance requires a game exposing a set of control methods. To see the required methods look at `ple/games/base.py`. 

Here's an example of importing Pong from the games library within PLE:

```python
from ple.games.originalGame import originalGame

game = originalGame()
```

Next we configure and initialize PLE:

```python
from ple import PLE

p = PLE(game, fps=30, display_screen=True, force_fps=False)
p.init()
```

The options above instruct PLE to display the game screen, with `display_screen`, while allowing PyGame to select the appropriate delay timing between frames to ensure 30fps with `force_fps`.

You are free to use any agent with the PLE. Below we create a fictional agent and grab the valid actions:

```python
myAgent = MyAgent(p.getActionSet())
```

We can now have our agent, with the help of PLE, interact with the game over a certain number of frames:

```python

nb_frames = 1000
reward = 0.0

for f in range(nb_frames):
	if p.game_over(): #check if the game is over
		p.reset_game()

	obs = p.getScreenRGB()
	action = myAgent.pickAction(reward, obs)
	reward = p.act(action)

```

Just like that we have our agent interacting with our game environment.

## Installation

PLE requires the following dependencies:
* numpy
* pygame
* pillow

Clone the repo and install with pip.

```bash
git clone https://github.com/ntasfi/PyGame-Learning-Environment.git
cd PyGame-Learning-Environment/
pip install -e .
``` 

## Headless Usage

Set the following in your code before usage:
```python
os.putenv('SDL_VIDEODRIVER', 'fbcon')
os.environ["SDL_VIDEODRIVER"] = "dummy"
```
