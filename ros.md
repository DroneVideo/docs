# ROS Noetic

## Overview

In our project, we use ROS (Robot Operating System) to reliably send information to our drone path control. ROS uses a network of publisher and subscriber nodes within a ROS topic to exchange data in real time. Another advantage of using ROS is its ability to access all the different hardware components on the drone.

While our object tracking algorithm publishes information about the position of the rover to the object_tracking topic, drone control path planning subscribes, receiving the relative coordinates and distance to the rover.

## Installation

ROS Noetic is intended for Ubuntu 20.04, which is what we are using as of Spring 2023. The installation goes as follows:

1.  Setup your computer to accept software from packages.ros.org.

    ```shell
    sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
    ```

2. Setup keys

```shell
sudo apt install curl # if you haven't already installed curl
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
```

3. Full Desktop Install

Make sure package index is up to date

```shell
sudo apt update
```

```shell
sudo apt install ros-noetic-desktop-full
```

4. Source ROS

```shell
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```