# Practical 6: Pixhawk and PX4, Commercial and R&D Autonomous Drone Systems

[TOC]

## Overview
Pixhawk and PX4 are widely used in autonomous drone development, providing an open-source hardware and software ecosystem for UAV control. In this tutorial, we will introduce:

- **Pixhawk**: The hardware autopilot platform
- **PX4**: The open-source flight control firmware
- **How to set up and use PX4 with Pixhawk**
- **PX4 Hardware In The Loop (HITL) Testing**

This will help you transition from Crazyflies and Aerostack2 to more advanced UAV platforms.

## What is Pixhawk?

Pixhawk is a family of open-source flight controllers developed for UAVs and robotics applications. It provides:

- High-performance **autopilot capabilities**
- **Multiple sensor support** (GPS, IMUs, barometers, etc.)
- **Compatibility** with PX4 and ArduPilot firmware
- Connectivity options like **UART, I2C, CAN, MAVLink and DDS**

### Common Pixhawk Versions:

- **Pixhawk 4**: Standard for academic and research use
- **Pixhawk 6X**: More advanced processing capabilities
- **Pixhawk 6C**: Compact version with strong processing power
- **Pixhawk Mini**: Compact version for small UAVs

### How to use a Pixhawk

This is the pixhawk 6c you will be playing around with, see all of the ports for various inputs

![pixhawk6c](images/Pixhawk6C.png)


This following wiring diagram is from an older pixhawk model, but should show the key elements of connecting up and powering a pixhawk 

![wiring](images/pixhawk_connect_essential_peripherals.jpg)

## Flight Control Firmware

There is no universal controller design of converting from user inputs to motor thrust. In the same way, there are numerous other functionalities that an autopilot can cover. These can range from running control loops for gimbals, cameras and other actuation, to high level mission following and safety features. These functionalities are bundled into specific autopilot *firmwares* which each offer a slightly different set of features, as well as differing user interfaces each with their advantages and drawbacks.

The two current most common autopilot firmware's in use in research settings are [Ardupilot](https://ardupilot.org/copter/index.html) which offers the Arducopter firmware, and [PX4](https://px4.io/) which offers Multicopter firmware. Both these firmwares are very extensive and cover numerous use cases. However, for our purposes we will only cover enabling autonomous flight through observing the *mode* of the autpilot.

Both Ardupilot and PX4 use the concept of flight modes, where each mode operates a supports different levels or types of flight stabilisation and/or autonomous functions. Traditionally this is for pilots to change between different controller layouts for different applications. It's necessary to change to the correct mode for safe and controllable flight. The following table shows the most often used flight modes within Starling.

| [Ardupilot Mode](https://ardupilot.org/copter/docs/flight-modes.html) 	| [PX4 Mode](https://docs.px4.io/v1.12/en/getting_started/flight_modes.html)  	| Functionality                                                                                 	|
|----------------	|-----------	|-----------------------------------------------------------------------------------------------	|
| stabilized     	| manual    	| Full manual control with RC sticks being sent directly to control roll, pitch, yaw and height 	|
| PosHold        	| position  	| UAV uses onboard sensing to stay in place, RC sticks used to translate position               	|
| loiter         	| auto.hold 	| Automatic mode where UAV stays in the same location until further instructions given.         	|
| land           	| auto.land 	| Automatic mode which attempts to land the UAV                                                 	|
| Guided         	| offboard  	| Navigates to setpoints sent to it by ground control or companion computer                     	|


As mentioned before, the base purpose of the firmware is to provide a given cascading PID controller for converting high level commands to motor thrusts. However both firmwares provide a plethora of other functionality from trajecotry following, basic mission following, telemetry and communications and many others too. 

As a controller developer, it is also useful to understand the differences between the Ardupilot and PX4 controllers and what real world impacts that has. In most of drone targeted applications we only require either position or velocity control which works fairly consistently between the two firmwares. 

In our own work, it has generally been noted that Ardupilot seems to be more suitable for outdoor flight, and PX4 for indoor flight. For this tutorial we will be developing a controller for indoor multi-vehicle flight and so we will assume the use of PX4. The biggest difference is actual in licensing where Ardupilot's license specifies that any developments must be contributed back, however PX4 is a bit more free allowing the forking and commercialisation without needing the announce or contribution (although this is not necessarily the best for the longevity of this open source project!). 

## PX4 Software Stack

PX4 consists of:
1. **PX4 Firmware** - The core flight control software
2. **QGroundControl (QGC)** - GUI for setup and mission planning
3. **MAVSDK (or other communication method)** - API for developing drone applications
4. **Hardware-In-The-Loop (HITL)** - Using real Pixhawk hardware for simulation or **Software-In-The-Loop (SITL)** for using simulated drones for testing. 


### Autopilot communication

Once in guided or offboard mode, the autopilot by default expects communications using the [MAVLINK protocol](https://mavlink.io/en/messages/common.html). Traditionally this would have been used for a ground control station (GCS) to send commands to a UAV over a telemetry link. However, now it has also developed into a protocol for commanding the autopilot from an onboard companion computer over a USB or serial connection too. The MAVLink protocol is a set of preset commands which compatible firmwares understand and react to. In this tutorial we will primarily be observing the mavlink interface, but we will not get into writing your own software with mavlink yet.

With the growing prevelance of ROS2, all of the major firmwares have attempted to provide direct communication using ROS2's underlying communication/middleware protocol of DDS (Data Distribution Service). Although we will not cover this in this module, this is what we currently use to communication between a companion computer and the pixhawk for drone work. 

Note however that even if DDS is enabled, autopilots will still send Mavlink messages down a *Telemetry* stream - often a dedicated low bandwidth communication channel for the monitoring of the drones health and status. 

### Ground Stations 



