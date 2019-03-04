# RoboND2_Proj4_DeepRL
ChrisL 2019-03-05

<img src="https://github.com/dusty-nv/jetson-reinforcement/raw/master/docs/images/gazebo_arm.jpg">


This repo is for personal coursework.<br/>
It is for the "Deep reinforcement" robotic arm ros project, 
the fourth project of Udacity Robotic Engineer ND, Term2.

## Submission notes
NOTE: This repo contains more than just the Catkin source directory!
The ROS source directory is <br>
$REPO/catkin_ws/src

The project report is [report.pdf](./report/report.pdf)<br/>

## Robot learning goals:
1. Have any part of the robot arm touch the object of interest, with at least a 90% accuracy.
2. Have only the gripper base of the robot arm touch the object, with at least a 80% accuracy.

## USAGE:

### Building from Source (Nvidia Jetson TX2)

Run the following commands from terminal to build the project from source:

``` bash
$ sudo apt-get install cmake
$ git clone http://github.com/udacity/RoboND-DeepRL-Project
$ cd RoboND-DeepRL-Project
$ git submodule update --init
$ mkdir build
$ cd build
$ cmake ../
$ make
```

During the `cmake` step, Torch will be installed so it can take awhile. It will download packages and ask you for your `sudo` password during the install.

### Testing the API

To make sure that the reinforcement learners are still functioning properly from C++, a simple example of using the API called [`catch`](samples/catch/catch.cpp) is provided.  Similar in concept to pong, a ball drops from the top of the screen which the agent must catch before the ball reaches the bottom of the screen, by moving it's paddle left or right.

To test the textual [`catch`](samples/catch/catch.cpp) sample, run the following executable from the terminal.  After around 100 episodes or so, the agent should start winning the episodes nearly 100% of the time:  

``` bash
$ cd $REPO/build/aarch64/bin
$ ./catch 
[deepRL]  input_width:    64
[deepRL]  input_height:   64
[deepRL]  input_channels: 1
[deepRL]  num_actions:    3
[deepRL]  optimizer:      RMSprop
[deepRL]  learning rate:  0.01
[deepRL]  replay_memory:  10000
[deepRL]  batch_size:     32
[deepRL]  gamma:          0.9
[deepRL]  epsilon_start:  0.9
[deepRL]  epsilon_end:    0.05
[deepRL]  epsilon_decay:  200.0
[deepRL]  allow_random:   1
[deepRL]  debug_mode:     0
[deepRL]  creating DQN model instance
[deepRL]  DQN model instance created
[deepRL]  DQN script done init
[cuda]  cudaAllocMapped 16384 bytes, CPU 0x1020a800000 GPU 0x1020a800000
[deepRL]  pyTorch THCState  0x0318D490
[deepRL]  nn.Conv2d() output size = 800
WON! episode 1
001 for 001  (1.0000) 
... 
WON! episode 112
080 for 112  (0.7143)  20 of last 20  (1.00)  (max=1.00)
```

Internally, [`catch`](samples/catch/catch.cpp) is using the [`dqnAgent`](c/dqnAgent.h) API 
from our C++ library to implement the learning.


### Runtime Environment
To get started with the project environment, run the following:

``` bash
$ cd $REPO/build/x86_64/bin
$ ./gazebo-arm.sh
```

The plugins which hook the learning into the simulation are located in the `gazebo/` directory of the repo. 
The RL agent and the reward functions are to be defined in [`ArmPlugin.cpp`](gazebo/ArmPlugin.cpp).

This project is based on the Nvidia open source project "jetson-reinforcement" developed by [Dustin Franklin](https://github.com/dusty-nv). The goal of the project is to create a DQN agent and define reward functions to teach a robotic arm to carry out two primary objectives:

### Common problems
Missing dependencies during build.

```
>> /usr/local/include/ignition/math/MassMatrix3.hh:477:19: error: 'IGN_MASSMATRIX3_DEFAULT_TOLERANCE' was not declared in this scope
sudo apt-get install libignition-math2-dev
``` <br/>
or  <br/>
```$REPO/bin/freshws.bash```

## Links
Submission Requirements: [Rubric](https://review.udacity.com/#!/rubrics/1441/view)
```commandline
git clone https://github.com/cielsys/RoboND2_Proj4_DeepRL
``` 