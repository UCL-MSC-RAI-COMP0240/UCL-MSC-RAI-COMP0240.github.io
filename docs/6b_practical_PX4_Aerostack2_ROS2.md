# Practical 6b: Autonomous flight with Pixhawk, Aerostack2, ROS2

## Overview
This is an optional session in which you will be able to fly a real drone manualy and autonomously with the holistic software stack you have learned from this module (PX4,Aerostack2, and ROS2) in HereEast fly area. This session contains the following steps:

- **Step1**: Setup the simulation environment
- **Step2**: Test your mission script in the simulation environment
- **Step3**: Setup and bench test the real drone (qav250) in Here east flight arena
- **Step4**: Conduct your mission on the real drone 

## Step1: Setup the simuatlion environment
In order to conduct autonomously flight with a real drone at the end of this session, we need to simulate it beforehand out of reasons such as safety test and debugging. What we need for simualtion environmen here is the exact software stack we will use in the real drone. It combines flight control firmware (PX4), ROS2, Aerostack2. In addition, we will use Gazebo as simulator for this time.

### Install ROS2 humble and Gazebo

Please refer to ROS2/Gazebo Fortress installation guide in [PRACTICAL1](https://ucl-msc-rai-comp0240.github.io/1c_intro_ros2/#).

### Install PX4

Please refer to PX4 installation guide in [PRACTICAL6](https://ucl-msc-rai-comp0240.github.io/6_practical_pixhawk_PX4/#using-px4-in-hitl-hardware-in-the-loop-simulation).

### Install Aerostack

Please refer to Aerostack2 installation guide in [PRACTICAL2-5.2Aerostack2 Installation](https://ucl-msc-rai-comp0240.github.io/2_practical_gazebo_aruco/).

### Setup the project
In this session, we will use anonther aerostack2 project called project_mavlink which allows PX4 communicating with ROS2 through MAVROS bridge. We made some modification to the original project, so please use our github repo instead of the original one.

Get the project locally:

```bash
mkdir -p ~/project_gazebo_ws/src
cd ~/project_gazebo_ws/src
git clone https://github.com/UCL-MSC-RAI-COMP0240/project_mavlink.git
```
## Step2: Test your mission script in the simulation environment

Launch the aerostack2:

```bash
cd ~/project_gazebo_ws/src/project_mavlink
./launch_as2_gazebo.bash -n qav1
```
Start the PX4 SITL, it will launch the gazebo automatically:

```bash
cd PX4-Autopilot
make px4_sitl gz_x500
```

Run the mission file: navigate to the mission monitoring panel by using ctrl+b and arrow keys ↑ ↓ ← →, and then 

```bash
python3 mission.py
```

Stop the aerostack:

```bash
cd ~/project_gazebo_ws/src/project_mavlink
./stop_tmuxinator_as2_gazebo.bash
```

## Step3: Setup and bench test the real drone (qav250) in Here east flight arena
Now we are ready to deploy our software stack onto a real drone and conduct a real flight. You will need to book a slot to UCL Here east flight area for the drone flight. Please use the following link to book. (Will add in soon)

1.Get safety induction

2.Familiarize yourself with infrastructure of UCL Here east Flight arena

3.Familiarize yourself with the drone

4.Bench testing

## Step4: Conduct your mission on qav250 
Before running your mission file, we need to ensure the drone's safety through manual flight and simple autonomously flight.

1.Manual fly in position mode

2.Autonomous fly with simple mission (just take off and land)

3.Autonomous fly with your mission file