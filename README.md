[![License](https://img.shields.io/badge/License-BSD%203--Clause-blue.svg)](https://opensource.org/licenses/BSD-3-Clause)
## ENPM808X ROS BEGINNER TUTORIALS
This is an implementation of publisher and subscriber node in ROS using 
http://wiki.ros.org/ROS/Tutorials/WritingPublisherSubscriber%28c%2B%2B%29

## Dependencies
This project requires ROS Kinetic and catkin running on Ubuntu 16.04 LTS
To install ROS Kinetic:
http://wiki.ros.org/kinetic/Installation
To install catkin: 
It gets installed by default alongwith ROS
else:  http://wiki.ros.org/catkin

## Build Steps
If you have ROS Kinectic and catkin installed: 
```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws
catkin_make 
source devel/setup.bash
cd src/
git clone https://github.com/s-niket/beginner_tutorials
cd ..
catkin_make
source devel/setup.bash
```

## Execution Steps
Open three terminals 

Terminal 1 (To run Master server)
```
roscore
```

Terminal 2 (To run Publisher Node)
```
cd ~/catkin_ws
catkin_make
source devel/setup.bash
rosrun beginner_tutorials talker
```
Terminal 3 (To run Subscriber Node)
```
cd ~/catkin_ws
catkin_make
source devel/setup.bash
rosrun beginner_tutorials listener
```
