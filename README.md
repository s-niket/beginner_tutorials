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
git clone -b Week10_HW --single-branch https://github.com/s-niket/beginner_tutorials.git
cd ..
catkin_make
source devel/setup.bash
```

## Execution Steps ( Without launch file)
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
Press Ctrl+C in each terminal to stop the execution

### Add custom message using rosservice
Execute the files and then open a new terminal and type:
```
cd ~catkin_ws
catkin_make
source devel/setup.bash
rosservice call /updateText <enter-text>
```
Example:
```
rosservice call /updateText Hello ROS!
```

After entering the text, you will notice the change in the message. 

### Execution Steps ( With launch file)
```
cd ~/catkin_ws
catkin_make
source devel/setup.bash
roslaunch beginner_tutorials Week10_HW.launch 
```

### Change Loop Frequency
Launch the file following the commands and then add the frequency parameter at the end:
```
cd ~/catkin_ws
source devel/setup.bash
roslaunch beginner_tutorials Week10_HW.launch frequency:=<any integer above zero>
```
Example:
```
roslaunch beginner_tutorials Week10_HW.launch frequency:=10
```
