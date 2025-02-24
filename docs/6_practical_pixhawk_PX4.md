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

A key element of any drone operation is a competent and reliable ground station setup. The purpose of the ground station is to provide a reliable communication link with the drone and receive telemetry to be able to keep an eye on, and monitor the status of the drone. Often this is done via a second *telemtry* radio operating on a different frequency - in our case an SIK radio on 433Mhz - with one end connected to the drone, and the other connected via USB to a laptop or computer (or handheld games console like the steam deck). 

There are a number of choices for a piece of software which runs on the ground station. In industry, you may see Alterion or other softwares which provide an interface. In the open source world we either use *mission planner* with Ardupilot or *QGroundContrl* with PX4. In this tutorial we will trying to use **QGroundControl** (QGC). 

![QGC](images/QGC.png)


Tools like QGC are crucial for real-time **flight monitoring, control, and mission planning**. It allows users to:

- **Monitor telemetry data** (battery levels, GPS status, IMU readings, etc.).
- **Send flight commands** such as takeoff, landing, and mission execution.
- **Configure drone parameters** including PID tuning, sensor calibrations, and failsafe settings.
- **Visualize the drone's location** and trajectory on a map interface.
- **Log and analyze flight data** to debug issues or optimize performance.

Ground stations are useful as they enable:

- **Safety**: Enables real-time monitoring, preventing potential failures.
- **Ease of Use**: Provides a user-friendly interface to interact with the drone.
- **Flexibility**: Supports different flight modes (manual, autonomous, guided, etc.).
- **Data Logging**: Essential for post-flight analysis, AI training, and debugging.
- **Remote Control**: Operate the drone without requiring direct physical interaction.

## Setting Up Pixhawk with PX4 and QGroundControl

Now lets setup your pixhawk with PX4, connect to it and do some initial calibrations with QGC. 

### Setup Overview

1. Install **QGroundControl (QGC)** ([Download](https://qgroundcontrol.com/))
2. Flash **PX4 firmware** onto Pixhawk via QGC
3. Configure **sensors and RC calibration**
4. Use *QGC* to setup some automated flights
5. (Not today) Setup **offboard control** (for AI/robotics integration)


### Install QGroundControl

Follow the following instructions for all platforms:

- [https://docs.qgroundcontrol.com/master/en/qgc-user-guide/getting_started/quick_start.html](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/getting_started/quick_start.html)

### Power up and connect the Pixhawk

Tidly unbox the pixhawk box in a way that you can put everything back later! For this tutorial, all you will need is:

- Pixhawk
- USB-C cable

Plug the USB-C cable from the Pixhawk to a port in your laptop

Now start QGroundControl

In the top left it will hopefully automatically pick up the pixhawk and you can start browsing the settings and seeing the live view. 

See [https://docs.qgroundcontrol.com/master/en/qgc-user-guide/getting_started/quick_start.html](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/getting_started/quick_start.html) for how to navigate and use QGC.

### Flashing the Pixhawk

The first step for us is to flash the latest PX4 version onto the pixhawk. This can be done easily from within QGC. 

Follow the following instruction page:

- [https://docs.qgroundcontrol.com/master/en/qgc-user-guide/setup_view/firmware.html](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/setup_view/firmware.html)


### Sensor Calibration 

The next step would be to perform sensor calibration in order to calibrate the onboard accelerometer and gyroscope. In the setup menu go to the sensors tab and follow the instructions. 

> Of course in practice you would perform the calibration after having built the drone, but this will do for now!

### Continue Setup

Scroll through the other setup steps, there are a number that we are skipping in this session, but in practice you would have to usually complete:

- **Radio Setup**: It's standard to have a radio connected with both a receiver connected to the pixhawk and a transmitter with the dedicated pilot. The radio is important in order to have a backup method of controlling the drone, as well enabling mode switching between various manual flight regimes and offboard mode. Important for safety too as having a emergency stop setup is highly recommended 
- **Safety Setup**: All the different safety systems built int from *return to home* to parachutes if they're installed. 
- **Parameters**: All of these setup screens essentially manipulate the value of various parameters under the hood. Have a scroll through the parameter list and you will quickly see that there are a lot of options for a variety of scenarios. Bare in mind that PX4 is highly multi-functional as it has been written to work on anything from fixed-wing aircraft to mini-submarines! 

> You might want to try setting up the virtual joystick to enable easier testing! [Joystick](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/setup_view/joystick.html) Note the PX4 instruction

### Next step

So once the setup is complete, the last thing to have a look at is observing some of the mavlink thats coming through 

Go have a look at the Analyse View: [analyse view](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/analyze_view/), and then the [mavlink inspector](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/analyze_view/mavlink_inspector.html)

However you will note that because we have a "drone" (just the pixhawk sitting on your desk that wont fly) you wont really be able to do much with it. Traditionally we would use Software In The Loop testing to simulate a virtual Pixhawk for testing and development. However in this class we would like to try and use Hardware-In-The-Loop testing to "fly" your drone. 


## Using PX4 in HITL (Hardware-In-The-Loop) Simulation

Instead of running Software-In-The-Loop (SITL), we will use **HITL** with Pixhawk 6C and QGroundControl. This avoids computer setup issues for software while allowing real-time testing on actual hardware.

### Steps to Run PX4 HITL:

1. Connect **Pixhawk 6C** to QGroundControl via USB.
2. In **QGroundControl**, navigate to *Simulation > HITL Configuration*.
3. Enable **HITL mode** and select your vehicle type.
4. Use **MAVLink telemetry** for monitoring real-time flight behavior.
5. Run tests and develop algorithms without needing a full drone setup.

### Benefits of HITL:

- Eliminates **computer setup issues** related to SITL.
- Uses **real Pixhawk hardware** for more accurate testing.
- Supports **custom AI and robotics applications**.

## Tasks


## Summary

For more details, refer to the [PX4 Developer Guide](https://docs.px4.io/).