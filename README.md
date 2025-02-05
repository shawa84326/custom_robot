# Custom Robot Simulation in Gazebo

## Overview
This project simulates a **custom cleaning robot** in Gazebo. The robot is based on the **Create Robot** as the base chassis and includes:
- A **trunk-like structure** for bio-waste suction.
- A **camera** for detecting bio-waste.
- Simulation of navigation and workflow in a **Gazebo environment**.

## Prerequisites
Ensure you have the following installed:
- **Ubuntu 20.04 or later**
- **ROS Noetic** (or appropriate ROS version)
- **Gazebo**

## Installation Steps

### 1. Create a ROS Workspace (if not already created)
```bash
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src
catkin_create_pkg custom_robot urdf gazebo_ros
cd ~/catkin_ws
catkin_make
```

### 2. Add the URDF File
Save the provided `custom_robot.urdf` file inside the `urdf` folder in your ROS package:
```bash
mkdir -p ~/catkin_ws/src/custom_robot/urdf
nano ~/catkin_ws/src/custom_robot/urdf/custom_robot.urdf
```
Paste the URDF content and save the file.

### 3. Create a Launch File
Navigate to the `launch` directory and create a `robot.launch` file:
```bash
mkdir -p ~/catkin_ws/src/custom_robot/launch
nano ~/catkin_ws/src/custom_robot/launch/robot.launch
```
Paste the following content:
```xml
<launch>
    <param name="robot_description" command="$(find xacro)/xacro $(find custom_robot)/urdf/custom_robot.urdf" />
    <node name="spawn_urdf" pkg="gazebo_ros" type="spawn_model" args="-param robot_description -gazebo -model custom_robot" />
</launch>
```
Save the file and exit.

### 4. Build the Workspace
```bash
cd ~/catkin_ws
catkin_make
source devel/setup.bash
```

### 5. Launch in Gazebo
Run the following command to spawn the robot in Gazebo:
```bash
roslaunch custom_robot robot.launch
```

## Expected Output
- A **blue cylindrical base** representing the Create Robot.
- A **gray trunk structure** for suction mounted on top.
- A **black camera** above the trunk for detecting bio-waste.
- The robot should appear inside the Gazebo environment and be ready for navigation simulation.

## Next Steps
- Implement **navigation** using ROS and Gazebo plugins.
- Integrate **bio-waste detection algorithms** using the camera sensor.
- Develop a **control interface** for interaction.

For modifications or improvements, update the `custom_robot.urdf` file accordingly. 🚀

