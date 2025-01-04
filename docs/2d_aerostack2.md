# Practical 2: Aerostack2 Framework For Aerial Robotic Systems  

[TOC]

## Robotic Frameworks For Aerial Control

As robotic and autonomous systems proliferate into the wider world, there is a need to address the difficulties of system development and deployment at scale. There is evidence that industry is directly facing these challenges through the use of cloud computing, continuous integration and similar systems inspired from very successful and agile software development processes. This is made clear through offerings such as Amazon's [AWS Robomaker](https://aws.amazon.com/robomaker/), Google's cloud robotics [platforms](\url{https://googlecloudrobotics.github.io/core/) and so on.

However, there is a great lack of such systems in most academic settings. The result's oriented attitude of many labs often leads to each researcher building a bespoke solution in order to evaluate, validate or prove their goals. These bespoke solutions are often inflexible, not extensible, difficult to understand and, importantly, reuse, with any level of confidence. This becomes especially difficult when coupled with hardware, such as UAVs, where many operational details have been implicitly assumed or ignored for favour of getting the experiment running as quick as possible. In addition these solutions are often poorly structured and maintained  with little to no documentation meaning that it is difficult for researchers to build upon these systems. This is an exceptionally large hurdle to researchers who do not have strong software backgrounds, but wish to perform real world experiments which could improve the quality of research outputs.

This is not to say that it is impossible for a research system to be developed into a reusable platform. There are many examples of research systems being ubiquitous within a group or being released outside the lab. For instance, the [Robotarium at Georgia Tech](https://www.robotarium.gatech.edu/), the Multi-Robot Systems Group at the Czech Technical University with their [experimental system](https://github.com/ctu-mrs/mrs_uav_system), and the PX4 autopilot which began it's life as a collaboration between a number of labs at ETH Zurich. But what we see is that it takes a concerted effort and many years of coincidental work which provide incremental improvements to the system each time. Previously I had attempted to develop a system which solved this problem called [starling](https://github.com/StarlingUAS/ProjectStarling) which had a number of flaws. 

Therefore as an example system for you to learn, we have chosen the **aerostack2** as our aerial robotic systems development platform. This will enable the following:

1. Supports single or multiple drones with low (control) or high level (path planning) experimentation.
2. Supports the transition between simulation to indoor flight to outdoor flight.
3. Provides a simple and easy to use interface for researchers to implement experimentation without knowledge of hardware specifics.

We hope that through using aerostack2, you develop an overview of the components required in an aerial system, and gain experiences which can then be applied to whatever systems you work with in the future.  

## Aerostack2 


