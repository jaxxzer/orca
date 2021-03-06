# Orca #

Orca is a [ROS](http://ros.org) driver for [BlueRobotics BlueROV2](https://www.bluerobotics.com/store/rov/bluerov2/) and [BeagleBone Blue](https://beagleboard.org/blue). Version 1.0 will support ROV functions; subsequent versions will add AUV functions.

## Hardware Requirements

* [BlueRobotics BlueROV2](https://www.bluerobotics.com/store/rov/bluerov2/) or similar ROV. The BlueROV2 has 6 thrusters in a 4-DOF vectored configuration, but you can modify the code to support other hardware platforms.
* [BeagleBone Blue](https://beagleboard.org/blue) controller. This replaces the Pixhawk2 controller that comes with the BlueROV2.
* Xbox One gamepad, or another device that's supported by the ROS joystick controller.

## Install

*Current status: Orca runs in [Gazebo](http://gazebosim.org/), a SITL (software-in-the-loop) simulator. Use the instructions below to install ROS, Gazebo and Orca.*

Install [ROS Kinetic](http://wiki.ros.org/Installation/Ubuntu). Select `ros-kinetic-desktop-full`; this will install Gazebo 7.0 as well.

Install these additional packages:
~~~~
sudo apt install ros-kinetic-pid
~~~~

Create a catkin workspace:
~~~~
source /opt/ros/kinetic/setup.bash
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
catkin_make
source devel/setup.bash
~~~~

Download and compile Orca:
~~~~
cd ~/catkin_ws/src
git clone https://github.com/clydemcqueen/orca.git
cd ..
catkin_make
~~~~

Run the simulation:
~~~~
roslaunch orca_gazebo orca.launch
~~~~

Plug in your gamepad, hit the [menu button](https://support.xbox.com/en-US/xbox-one/accessories/xbox-one-wireless-controller) to arm the thrusters and start driving around.

Here's how the buttons are mapped:
* Left stick up/down is forward/reverse
* Left stick left/right is yaw left/right
* Right stick up/down is ascend/descend
* Right stick left/right is strafe left/right
* Menu button: arm
* View button: disarm
* A button: manual
* X button: hold yaw
* Y button: hold yaw and depth
* B button: go to surface and hold yaw and depth

## Code Structure

There are 3 projects:
* `orca_base` provides the ROV and AUV code
  * `orca_driver.cpp` runs on the BeagleBone Blue and provides an interface between the hardware and ROS messages.
  * `orca_base.cpp` runs on any ROS device and provides ROV and AUV functionality.
* `orca_description` provides the robot description files.
* `orca_gazebo` provides the simulation environment.