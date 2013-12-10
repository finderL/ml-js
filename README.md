ml-js
====

Machine Learning library for Node.js

Status : Under development, v0.0.3

## Installation
ml-js depends on [FANN](http://leenissen.dk/fann/wp/) (Fast Artificial Neural Network Library) witch is a free, open source and high performence neural network library.

To build great app with it : 
* Make sure you glib2 is installed  : `sudo apt-get install glib2.0`
* make sure pkg-config is installed : `sudo apt-get install pkg-config`
* make sure cmake is installed      : `sudo apt-get install cmake`
* Install FANN : 
  * download  [here](http://leenissen.dk/fann/wp/download/)
  * unzip
  * goto to FANN directory
  * run `cmake .` and `sudo make install`
  * run `sudo ldconfig`

Finally, you should be able to install all npm dependancies :  `npm install ml-js --save`

## Supported ML techniques
ml-js currently supports : 
* Supervised learning :
  * Neural Networks through FANN library
* Reinforcement learning :
  *  QLearning
    *  Continuous states (als called features) / discete actions 
  *  Exploration policies
    *  BoltzmannExploration

## Getting started

### QLearning pseudo code 
[Q-learning](http://en.wikipedia.org/wiki/Q-learning) is a model-free reinforcement learning technique. Specifically, Q-learning can be used to find an optimal action-selection policy for any given [MDP](http://en.wikipedia.org/wiki/Markov_decision_process).

```coffeescript
mljs = require 'ml-js'
utils = require 'utils' 
EventEmitter = require('events').EventEmitter

myprocess = new SomeProcess
utils.inherits SomeProcess, EventEmitter 


qValues = new mljs.ContinuousQValues nb_features, nb_actions

options = {
  learning_rate: 0.1
  discount_factor: 0.9
  exploration_policy: new mljs.BoltzmannExploration 0.2 # temperature 
}
agent = new mljs.QLearningAgent qValues, options

myprocess.on 'do_something', (current_state)->
  next_action_index = agent.getAction current_state
  next_action = actions[next_action_index]
  myprocess.do next_action
  
myprocess.on 'feedback_received', (init_state, action_index, new_state, reward)->
    agent.learn init_state, action_index, new_state, reward, (info)->
      console.log info
```