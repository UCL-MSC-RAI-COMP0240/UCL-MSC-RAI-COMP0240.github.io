# Practical 1: First time flight

[TOC]

## Before you fly

At this point, the crazyflie will have no external sensors and will rely on its internal odometry to keep itself stable. 

**BEFORE YOU FLY PLEASE READ THE FOLLOWING**

**WARNING** 

- If the loco board or flow board is installed, the drone will be in position hold mode where it can hold still itself. If they are not the drone will be in **manual** flight mode and will have no ability to help you fly or stabilise **it will drift**. 
- The joysticks will be mapped directly to roll/pitch/yaw and thrust. 
- The joystcks control might be quite sensitive so use **small movements** until you get the hang of it
- You must be as smooth as you can with your joystick control - try not to twitch in the opposite direction when something happens - this results in a hard to recover drone! 
- Familiarise yourself with the location of the **emergency stop** if you feel uncomfortable press it at any time (the crazyflies can handle heavy landings)

To understand the coordinate system and roll pitch and yaw see the following link:
- [https://www.bitcraze.io/documentation/system/platform/cf2-coordinate-system/](https://www.bitcraze.io/documentation/system/platform/cf2-coordinate-system/)

When you are ready to fly, **notify an instructor** and place the crazyflie in the middle of your flying space. 

## Flying

The instructor will first check all is good with your drone and you have a good setup before you fly.

> **Note:** A batery only has around 5 minutes of flying time - keep an eye on it and swap it out if necessary. 

Just like being introduced to any new drone, you will first try to get a feel for how the drone will react to your control. Here is a list of actions you can go through to check and learn how your drone flies. 

1. Arming only test - In this test you will simply arm, wait a second, and then disarm he drone - you will *not* move the sticks. When you arm the drone, the motors will start spinning at minimum RPM, but not takeoff or otherwise move. Disarming the drone will then stop the motors. Does the drone arm and disarm again straight after without needing a restart

2. Arming ESTOP test - In this test you will familiarise yourself with, and ensure that the emergency stop button works. Arm the drone and then press the estop. The motors should stop and the GUI should show emergency stop has been pressed. 

3. Floor thrust test - In this test you will start to familiarise yourself with the thrust control of the controller and response from the drone. You will want to gently increase the thrust, and you should start to see the drone looking like it wants to get off the ground. Try and get a feel for its response! Also worth noting if the drone appears to pivot to one side instead of thrusting equally from all four motors - you may need to compensate a little using the yaw and pitch. 

4. Gentle Takeoff and Landing - In this test you will attempt to have the drone takeoff and gently land in a controlled fashion. Building upon the previous, you should gently increase thrust until the drone leaves the ground. When it leaves the ground, try and hold the right thrust level if you can, otherwise reduce the thrust and try and land softly on the ground. 
    - **Important** A lot of beginner flyers will jerk the stick when it takes off - either plunging it into the ceiling or floor. Try to avoid this by holding your nerve and staying in control. 
    - **If you feel out of control hit the ESTOP**
    - Landing Tip - Thust up a little bit just before you hit the floor, this will reduce the impact on the drone. 

5. Hovering - Once you are happy and in control with takeoff and landing, you should try and hold the hover for longer, correcting for horizontal drift using the roll/pitch correction. 
    - **If you feel out of control hit the ESTOP**

6. Controlled Flight (no yaw)- Hopefully at this point you should be feeling a lot more in control of the drone (but you probably need a bit of practice!). Now try and slowly fly some shapes (square, circle etc) with the drone always facing away from you (no yaw). 

7. Controlled Flight - Now try flying the same shapes, but this time using yaw instead of rolling, i.e. always facing in the direction you want to move. It is recommended you try this by first yawing on the spot then moving forward. When you get more confident, you will be able to yaw while moving - this is the closest you'll get to FPV flying in this course! 

> If working in a pair, don't forget to swap over!

> You may have noticed in the GUI and on the control scheme, there is a button labelled *Assist Mode* this will perform an automatic takeoff and activate hover mode as long as its pressed down. Read the Flow deck [tutorial](https://www.bitcraze.io/documentation/tutorials/getting-started-with-stem-drone-bundle/) for more information.  

Dont worry if you don't get through all of these maneouvers, these take practice to learn and master! The goal here is for you to have some hands on experience on what a flying vehicle is like and have some experience with the physical system before we start playing with autonomy. 

> If you want a challenge, remove the optical flow board / loco positioning board and try flying in manual mode **WARNING** you will have no automatic positioning or hovering - you will have to manually control this yourself. 


## Autonomous Flight

Having hopefully flown the drone manually, you should now be beginning to form some intuitions as to how a drone flies, its features, things to watch out for and so on. Now we move onto starting to consider a key part of this course - which is autonomy. 

Autonomy is a bit different for drones over other robots you may have used in the past. Unlike ground vehicles, we have to consider the effects of a 3rd dimension, and need some form of cascaded control to stay in the air. Also whilst the inverse kinematics calculations for arms are not necessary for drones - features such as smooth trajectory generation and following, and mission planning are neccesary. 

Thankfully, crazyflie offers a simple starting point with a python api for autonomous flight. This will get you back up to speed with programming and testing robots before we delve into more complex autonomous systems which you would see flavours of in the real world. Remember at the end of the day, all of these different frameworks are just tools - we hope that through learning to use these tools, you also absorb and learn more generalisable features of drone autonomy which you could apply to the many other open source and proprietary systems which exist out there!  

For crazyflie autonomy, try out the following links which show a simple getting started! 

- Flow Deck [tutorial](https://www.bitcraze.io/documentation/tutorials/getting-started-with-stem-drone-bundle/)
- Multi-Ranger Deck [tutorial](https://www.bitcraze.io/documentation/tutorials/getting-started-with-stem-ranging-bundle/)
- Loco Deck [tutorial](https://www.bitcraze.io/documentation/tutorials/getting-started-with-flying-using-lps/)
- Example Scripts [Link](https://github.com/bitcraze/crazyflie-lib-python/tree/master/examples)

**Your goal here is to have the drone fly in some shapes autonomosly**

> As a bonus, see if you can start to work out how to use the LED Deck! 

You will likely needed to look up a little of the documentation for the api but I'm sure you can mostly use the examples to work out the best way to program the drones to do what you need. Don't worry about making things too complicated, as we will be quickly moving on to ROS2 for drone control! 