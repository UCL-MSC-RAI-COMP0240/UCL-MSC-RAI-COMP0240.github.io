# Practical 1: Foundations: ROS2 with Aerostack2

In this first practical, you will be introduced to the core software ecosystem used for aerial robotics development in this course. The focus is on ROS 2 and Aerostack2, a ROS 2–based framework for the control, coordination, and autonomy of single and multiple drones.

This practical is foundational. It is designed to bring all students to a common baseline, regardless of prior experience with Linux, ROS 2, or drone software frameworks.

You are not expected to be an expert in these tools at the start. Instead, the aim is to understand how the different components fit together and to gain confidence navigating and modifying an existing aerial robotics software stack.

## Structure of Practical 1:
This practical is split into a series of guided pages. Depending on your background, you may progress through these at different speeds or skip sections where you already feel confident.

You are expected to complete the tasks individually and work through the associated checklist for this practical. Once you have completed the required tasks, you should demonstrate your progress to a course tutor, who will log your completion.

1. [Linux Installation](1b_intro_linux.md)
    - For students who do not yet have a working Ubuntu 22.04 installation, or who would benefit from a refresher on Linux basics.
    - Covers essential command-line usage and system navigation required for the rest of the course.
2. [ROS2 Installation](1c_intro_ros2.md)
    - For students who have not previously installed or used ROS 2 Humble.
    - Introduces core ROS 2 concepts and provides installation guidance for different platforms.
3. [Aerostack2](1d_aerostack2.md)
    - Introduces the Aerostack2 framework for aerial robotics.
    - Explains the system architecture and how Aerostack2 builds on top of ROS 2 to support drone autonomy, mission execution, and multi-agent coordination.
    - This framework will be used throughout the remainder of the course.
4. [Gazebo Aruco Mini-Challenge](2_practical_gazebo_aruco.md)
    - A short, hands-on challenge that brings together ROS 2, Aerostack2, and simulation.
    - You will implement a simple solution within Aerostack2 to solve a perception-driven task in Gazebo.
    - This serves as a first end-to-end example of an aerial robotics workflow.
    - The aim is to complete this challenge by the end of week 2.
![teleop](images/2_teleoperation.png)
