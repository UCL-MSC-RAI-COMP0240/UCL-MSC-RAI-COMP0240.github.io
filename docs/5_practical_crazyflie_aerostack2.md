# Practical 5: Crazyflie with aerostack2
In this fifth practical, we will reimplement manual flight and scripted autonomous flight of crazyflies via aerostack2. 

[TOC]

## Clond and build aerostack2 package: as2_platform_crazyflie


The first step is to clone and build another aerostack2 package called as2_platform_crazyflie.

Please follow the instructions here before aerostack2 common interface.

- [https://aerostack2.github.io/_03_aerial_platforms/_crazyflie/index.html](https://aerostack2.github.io/_03_aerial_platforms/_crazyflie/index.html)

**NOTE: Use source installation and clone the package in the src folder under your aerostack2 workspace.** 

**NOTE: The documentation may use the "git@.." and you may have issues with ssh. Go to the github repository and use the "https://..." version! 


## Clone project_crazyflie into your aerostack2 workspace

Then, you need to clone the project_crazyflie into your aerostack2 workspace.

Follow the instructions here.

- [https://github.com/aerostack2/project_crazyflie?tab=readme-ov-file](https://github.com/aerostack2/project_crazyflie?tab=readme-ov-file)

## Change radio channel in config file

To be able to connect to your crazyflie, you need to change the setting of radio channel in the package's config file.

Please read through instructions here. 

- [https://aerostack2.github.io/_02_examples/crazyflie/project_crazyflie/index​](https://aerostack2.github.io/_02_examples/crazyflie/project_crazyflie/index​)

## Teleoperate and autonomously fly crazyflie via aerostack2

Now, you should be able to lanuch the project, connect to, teleoperate, and autonomously fly your crazyflie. 

Follow instructions here.

- [https://github.com/aerostack2/project_crazyflie?tab=readme-ov-file​​](https://github.com/aerostack2/project_crazyflie?tab=readme-ov-file​​)

**NOTE: 1.Before launch any bash file, disconnect your crazyflie with your cfclient which may occupy the radio channel. 2. After each flight, you have to manually restart your crazyflie.** 

