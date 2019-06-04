# Installation

## Debians
For the installation of ROS 2 Dashing,
please refer to the online documentation :

[Linux-Install-Debians](https://index.ros.org/doc/ros2/Installation/Dashing/Linux-Install-Debians/)

## From sources
For downloading and setting up a full ROS 2 workspace,
please refer to the online documentation :

[Linux-Development-Setup](https://index.ros.org/doc/ros2/Installation/Dashing/Linux-Development-Setup/)

### Notice

#### Living on the edge

To get the bleeding edge state of the ROS 2 development, use the following

```terminal
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws
wget https://raw.githubusercontent.com/ros2/ros2/master/ros2.repos
vcs import src < ros2.repos
```

in the [Get ROS 2 code](https://index.ros.org/doc/ros2/Installation/Dashing/Linux-Development-Setup/#get-ros-2-code)
section of the installation procedure.

#### Updating a Crystal workspace

If you already had a ROS 2 workspace set up with the Crystal release,
you will have to delete the package `ament/osrf_pycommon` as it has been
moved to `osrf/osrf_pycommon` causing an error,

```terminal
ERROR: Rosdep experienced an error: Multiple packages found with the same name "osrf_pycommon":
- ament/osrf_pycommon
- osrf/osrf_pycommon
Please go to the rosdep page [1] and file a bug report with the stack trace below.
[1] : http://www.ros.org/wiki/rosdep
```

To do so, simply type in a terminal:

```terminal
cd ~/ros2_ws/
rm -r src/ament/osrf_pycommon
```
