# Flipping URDF Robot
## About This Package
### Creator
Cody Nichoson

### Overview 
This  package is called `diff_drive` and serves to create, simulate, and control a custom robot model created with URDF so that it performs flips in Gazebo.

## Video Demonstration Links
#### Flipping Robot in Gazebo
https://youtu.be/s7BYN_Po0b0

## Usage Instructions
### Part 1 - Flipping URDF Robot
1. Run the flipping robot launchfile using the command `roslaunch diff_drive ddrive.launch`.
2. Once Gazebo opens, press the play button at the bottom left of the screen.
3. Enjoy watching a cute wooden robot do some flips!

## Launchfiles and Nodes
### Launchfiles
**`ddrive.launch`**

Launches the robot model in `Gazebo` in a custom world map. 

**`ddrive_rviz`**

Launches the URDF robot in `rviz` to aid in link and joint editing.

### Nodes
**`flip`**

Publishes to `cmd_vel` repeatedly in opposite directions to encourage the robot to flip.
