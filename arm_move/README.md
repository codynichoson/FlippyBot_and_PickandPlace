# MoveIt! Manipulation Exercise
## About This Package
#### Creator
Cody Nichoson

#### Overview 
This package is called `arm_move` and utilizes MoveIt! to control a PincherX 100 robot arm and perform simple motion planning capabilities in both simulation and the real world.

## Video Demonstration Links

#### Simulated PincherX 100 Picking an Object Up (Obstacle Location 1)
https://youtu.be/jtutWcg3htY

#### Real PincherX 100 Picking an Object Up (Obstacle Location 1)
https://youtu.be/lrAWV9bWFnM

#### Real PincherX 100 Picking an Object Up (Obstacle Location 2)
https://youtu.be/2Zd_sR6jxTw

## Usage Instructions
### PincherX100 Manipulation Using MoveIt!
#### Note: These procedures assume that the Interbotix packages `interbotix_ros_core`, `interbotix_ros_manipulators`, and `interbotix_ros_toolboxes` have been installed.

#### Launching in Various Modes
1. To run the launchfile in visualization mode (Rviz only), run the command `roslaunch arm_move arm.launch use_fake:=true`.
2. To run the launchfile in simulation mode (Gazebo and Rviz), run the command `roslaunch arm_move arm.launch use_gazebo:=true`.
3. To run the launchfile in real mode (actual robot and Rviz), run the command `roslaunch arm_move arm.launch use_actual:=true`.

#### Controlling the Robot Arm Using Services
1. In another terminal window, type `rosservice call /px100/reset`, then hit the `Tab` button twice to auto-complete the input format 
for the `reset` service. Fill in appropriate coordinates for the location of a RealSense box obstacle (standing on end) relative to the 
center of the robot's base and whether or not you wish to clear the current list of waypoints (no waypoints initially). Calling the `reset` 
service using the inputs below will spawn a RealSense box standing on its end 15cm in front of the PincherX 100 and extend the arm to its 'Home' 
position.
```
rosservice call /px100/reset "box_pose:
  x: 0.15
  y: 0.0
  z: 0.0
clear_wp: false" 
```
2. To move the robot arm to some desired position, call the `step` service using the command `rosservice call /px100/step`, and hit the `Tab`
button twice to auto-complete the input format. For this input, you will type in the desired position of the robot's end-effector relative to
the center of the robot's base, as well as a gripper state (true for closed, false for open). Each successive position that is called will be 
added to a list of waypoints. An example input is:
```
rosservice call /px100/step "coordinates:
  x: 0.1
  y: 0.2
  z: 0.25
gripper: true" 
```
3. Finally, to have the robot arm iterate through a series of waypoints, call the `follow` service by typing the command `rosservice call /px100/follow` and hitting the `Tab` button twice to auto-complete the input format. This input takes two boolean values that determine how the robot will iterate through waypoints. To loop through one waypoint pattern continuously, set `repeat = True`. To loop through only once, set `repeat = False`. In addition, the argument `custom` allows you choose between a preset list of waypoints (located in the `.yaml` file) and custom waypoints (appended everytime the `step` service is called). Setting `custom = True` will use the waypoints from the `step` service, and setting `custom = False` will use waypoints from the `.yaml` file. An example input is:
```
rosservice call /px100/follow "repeat: false
custom: true" 
```

#### Configuration Changes
The waypoint path specified in the .yaml file can be adjusted by opening the file and changing the values in the `waypoints` list. The format of
each waypoint is `[x, y, z, gripper_state]` where `x`, `y`, and `z` are in meters and `gripper_state` is `True` for closed and `False` for open.

## Launchfiles and Nodes
### Launchfiles
**`arm.launch`**

Launches the PincherX 100 visualization in `rviz` if launched with `use_fake:=true`, `gazebo` if launched with `use_gazebo:=true`, or the real PincherX100 if launched with `uze_actual:=true`.

### Nodes
**`mover`**

Contains all the services used to move and manipulate the robot arm.



