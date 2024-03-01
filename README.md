# Guide for migrating TurtleBot 3 to ROS2 Humble

In this repository, a step-by-step guide for migrating the Robotis' TurtleBot 3 to ROS2 is presented 

![Turtlebot 3](https://github.com/RAS-UAO/turtlebot3/assets/98227139/0b90fbb5-28ae-497b-bc9f-ac5e382137af)

**Important:** The guides talks exclusively about *ROS2 Humble* distribution, no other ROS2 distributions such as Foxy or Iron.

# Part 1: Ubuntu Server 22.04 Installation

Please, install **Ubuntu Server 22.04** on the TurtleBot's Raspberry Pi 3.

**Unfortunately**, *in difference to Raspberry Pi 4*,  it's not factible to install the Desktop variant due to hardware limitations.

To install Ubuntu, it's recommended to follow the instructions in this link: https://ubuntu.com/tutorials/how-to-install-ubuntu-on-your-raspberry-pi#1-overview

**Warning:** The Wi-Fi that the Raspberry Pi 3 is configured will be the one with which it can be connected via SSH, you must be careful when selecting it.

# Part 2: ROS2 Humble Installation

Now, that Ubuntu is there, it's necessary to install ROS2 Humble in the Raspberry Pi 3,

In order to do that, the standard instructions for installing ROS works perfectly, the instructions are explained in this link: https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debians.html

# Part 3: TurtleBot 3's Packages Installation

Now that Ubuntu Server 22.04 and ROS2 Humble are available, it's time to set up the Raspberry Pi 3 to be used as Turtlebot 3's brain.

In order to do that, it's just necessary to install the Turtlebot 3's packages with this command line:

    sudo apt install ros-humble-turtlebot3*

# Part 4: TurtleBot 3's Physical Devices Componentes

Having Ubuntu, ROS and its necessary packages, the next step is to install the TurtleBot 3's physical devices to use the real robot.

The physical devices are:

 - LDS-01 LiDAR (or LDS-02 LiDAR, depending on the year the TurtleBot 3 was bought). It's possible to deduct the LiDAR model just by the looks:

![Captura de pantalla 2024-02-29 144446](https://github.com/RAS-UAO/turtlebot3/assets/98227139/9a7f1e50-21eb-4b69-9e53-1743a20bd5b8)

 
 - OpenCR board. This is the board that controls the TurtleBot 3's motors

![OpenCR](https://github.com/RAS-UAO/turtlebot3/assets/98227139/54392209-2545-4e75-b491-be876f82db5b)


To install the LDS-01 LiDAR (in our case), just type:

    sudo apt install ros-humble-hls-lfcd-lds-driver*

To install OpenCR's  firmware , it's recommended to follow the instructions in this link: 
https://emanual.robotis.com/docs/en/platform/turtlebot3/opencr_setup/#opencr-setup

**Warning:** Remember to include the instructions for the *Humble distribution* of ROS2, otherwise the installation will most likely not be effective.

# Part 5: Additional Raspberry Pi 3's set up

These next steps are absolutely necessary because, every time the TurtleBot 3 is used, the following commands must be executed:

    source /opt/ros/humble/setup.bash

    export ROS_DOMAIN_ID=11

    export TURTLEBOT3_MODEL=burger

    export LDS_MODEL=LDS-01

    export OPENCR_PORT=/dev/ttyACM0

    export OPENCR_MODEL=burger

Those are the ROS2 and hardware configurations to use the Turtlebot 3. Please, **the user's PC and the TurtleBot's Raspberry Pi must have the exact same ROS_DOMAIN_ID**, note that the ROS_DOMAIN_ID is recommended to be 0 or 11 for the TurtleBot 3

However, there is a way to not have to introduce those commands all the time: **to add them to the hidden *.bashrc file*.**

Please, enter the following commands in the terminal just *once*:

    echo 'source /opt/ros/humble/setup.bash' >> ~/.bashrc

    echo 'export ROS_DOMAIN_ID=11' >> ~/.bashrc

    echo 'export TURTLEBOT3_MODEL=burger' >> ~/.bashrc

    echo 'export LDS_MODEL=LDS-01' >> ~/.bashrc

    echo 'export OPENCR_PORT=/dev/ttyACM0' >> ~/.bashrc

    echo 'export OPENCR_MODEL=burger >> ~/.bashrc

    source .bashrc

Once these commands are added to the .bashrc file, they're executed when a terminal is opened. With these changes, those commands are executed automatically when opening a terminal.
