[![License](https://img.shields.io/badge/License-BSD%203--Clause-blue.svg)](https://opensource.org/licenses/BSD-3-Clause)
## ENPM808X ROS BEGINNER TUTORIALS ROS TF, Unit Testing, bag files
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
git clone -b Week11_HW --single-branch https://github.com/s-niket/beginner_tutorials.git
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
Use Ctrl+C to close the terminals 

### TF Frames
The Talker node broadcasts /talker frame which has a non-zero translation and rotation with respect to the /world frame. 
One can check the TF frames using tools tf_echo and rqt_tf_tree. The translation vector in the code uses 
random values generated between (0,100), hence the translation changes in every loop. Using tf_echo, we can see 
the values of translation and rotation vectors in the terminal, while the talker node is running on the other terminal. 
To run tf_echo, run talker node on one terminal by using above steps, and open another terminal and do:
```
rosrun tf tf_echo /world /talker
```
The translation and rotation vectors are displayed on the terminal. Use Ctrl+C to stop the tool.
rqt_tf_tree can be used to visualize the tree of frames being broadcasted. For that:
```
rosrun rqt_tf_tree rqt_tf_tree
```
For the diagram of broadcasted frames, use view_frames: 
```
cd ~/catkin_ws
rosrun tf view_frames
```
This command generates a pdf file the diagram, in the catkin_ws directory. We can view it by:
```
evince frames.pdf
```
### ROSTEST

To run test case for talker node, open a new terminal and:
```
cd ~/catkin_ws
catkin_make
source devel/setup.bash
rostest beginner_tutorials talkerTest.launch
```
The output of the test looks like:
```
rostest beginner_tutorials talkerTest.launch 
... logging to /home/niket/.ros/log/rostest-niket-G5-5587-17523.log
[ROSUNIT] Outputting test results to /home/niket/.ros/test_results/beginner_tutorials/rostest-test_talkerTest.xml
[Testcase: testtalkerTest] ... ok

[ROSTEST]-----------------------------------------------------------------------

[beginner_tutorials.rosunit-talkerTest/testTextUpdation][passed]

SUMMARY
 * RESULT: SUCCESS
 * TESTS: 1
 * ERRORS: 0
 * FAILURES: 0

rostest log file is in /home/niket/.ros/log/rostest-niket-G5-5587-17523.log
```

### ROSBAG
A .bag file will record all the published data. After running the Publisher/Subscriber node,we can view the 
full list of topics that are currently being published in the running system by running this in a new terminal:
```
rostopic list -v
```
The rosbag record with the option -a, indicating that all published topics should be accumulated in a bag file,
can be used to record all the published data.
```
rosbag record -a
```
To play back a .bag file, run the listener node in one terminal and in the other:
```
rosbag play <bag-file name>.bag
```
To enable/disable recording, use the following commands:
```
roslaunch beginner_tutorials Week11_HW.launch rosbagEnable:=true
```
