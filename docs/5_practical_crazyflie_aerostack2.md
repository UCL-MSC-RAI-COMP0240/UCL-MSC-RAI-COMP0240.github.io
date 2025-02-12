# Practical 5: Crazyflie with aerostack2
In this fifth practical, we will reimplement manual flight and scripted autonomous flight of crazyflies via aerostack2. 

[TOC]

## Clone and build aerostack2 package: as2_platform_crazyflie


First step is to clone and build another aerostack2 package called as2_platform_crazyflie.

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

This can be done by accessing the config/config.yaml: configuration file for the Crazyflie drones.

**NOTE: Make sure the radio channel set in the config file matches the channel you plan to use in the cfclient GUI, as done in the previous lab. Inconsistent channels will prevent the drone from connecting.** 

Please read through instructions here. 

- [https://aerostack2.github.io/_02_examples/crazyflie/project_crazyflie/](https://aerostack2.github.io/_02_examples/crazyflie/project_crazyflie/)

## Teleoperate and autonomously fly crazyflie via aerostack2

Now, you should be able to lanuch the project, connect to, teleoperate, and autonomously fly your crazyflie. 

Follow instructions here.

- [https://github.com/aerostack2/project_crazyflie?tab=readme-ov-file​​](https://github.com/aerostack2/project_crazyflie?tab=readme-ov-file​​)

**NOTE: 1.Before launch any bash file, disconnect your crazyflie with your cfclient which may occupy the radio channel. 2. After each flight, you have to manually restart your crazyflie.** 

**NOTE: 2. After each flight, you have to manually restart your crazyflie.If you find the Crazyflie remains unresponsive after a flight or changing configs, physically unplug the battery for a few seconds, then reconnect it.** 

**NOTE: 3. Always test your Crazyflie in an open, safe area free of obstacles, and with safety googles on, especially when first trying autonomous flight. Keep emergency stop in mind if something goes wrong.**