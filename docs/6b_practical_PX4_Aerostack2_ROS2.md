# Practical 6b: Pixhawk and PX4, Aerostack2, ROS2

##Overview
This is an optional session in which you will be able to fly a real drone manualy and autonomously with the holistic software stack you have learned in this module (PX4,Aerostack2, and ROS2) in HereEast fly area. This session contains the following steps:

- **Step1**: Setup the simulation environment
- **Step2**: Test your mission script in the simulation environment
- **Step3**: Setup the real drone (qav250)
- **Step3**: Test your mission file through autonomous flight

## Setup the simuatlion environment
In order to conduct autonomously flight with real drone at the end of this session, we need to simulate it beforehand out of reasons such as safety test and debugging. What we need for simualtion environmen here is the exact software stack we will use in the real drone. It combines flight control firmware (PX4), ROS2, Aerostack2. In addition, We will use Gazebo as simulator for this time.

### Install ROS2 humble and Gazebo

Please refer to ROS2/Gazebo Fortress installation guide in [PRACTICAL1](https://ucl-msc-rai-comp0240.github.io/1c_intro_ros2/#).

### Install PX4

Please refer to PX4 installation guide in [PRACTICAL6](https://ucl-msc-rai-comp0240.github.io/6_practical_pixhawk_PX4/#using-px4-in-hitl-hardware-in-the-loop-simulation).

### Install Aerostack

Please refer to Aerostack2 installation guide in [PRACTICAL2-5.2Aerostack2 Installation](https://ucl-msc-rai-comp0240.github.io/2_practical_gazebo_aruco/).

### Setup the project

