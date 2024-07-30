English| [简体中文](./README_cn.md)

# Function Introduction

OriginBot is an intelligent robot open source kit, and also a community co-built open source project, designed to let every participant enjoy the fun of robot development. This project is the minimum function system of OriginBot robot, which can accept /cmd_vel command to control robot movement and feedback /Odom information. This system includes the following three function packages:

- originbot_base: Robot chassis drive
- originbot_driver: Robot serial drive package
- originbot_msgs: OriginBot custom communication interface

# Bill of Materials

| Robot Name         | Manufacturer | Reference Link                                               |
| :------------------ | ------------ | ------------------------------------------------------------ |
| OriginBot Intelligent Robot | GuYueJu | [Purchase Link](https://www.originbot.org/)          |
| RDK X3 Robot        | Multiple Manufacturers | [Purchase Link](https://developer.horizon.ai/sunrise) |

# Instructions

## Preparation

Refer to the [user guide](https://www.originbot.org/guide/quick_guide/) on OriginBot robot's official website to complete the hardware assembly of the robot.

## Installation

Click on the upper right corner of the [NodeHub OriginBot project](http://it-dev.horizon.ai/nodehubDetail/170117036053371431) for fast deployment, connect to the robot through terminal or VNC, copy and run the following commands on the RDK system to install the minimal system of OriginBot robot.

tros foxy: 
```bash
sudo apt update
sudo apt install -y tros-originbot-base tros-serial tros-originbot-msgs
```
tros humble:
```bash
sudo apt update
sudo apt install -y tros-humble-originbot-base tros-humble-serial tros-humble-originbot-msgs
```

## Operation

### Start Robot

Enter the following command in the terminal:

tros foxy:
```bash
source /opt/tros/setup.bash
ros2 launch originbot_base robot.launch.py 
```
tros humble:
```bash
source /opt/tros/humble/setup.bash
ros2 launch originbot_base robot.launch.py 
```

After successful execution, you will see the following prompt

```shell
root@ubuntu:/userdata# ros2 launch originbot_base robot.launch.py
[INFO] [launch]: All log files can be found below /root/.ros/log/2023-07-09-16-49-58-754723-ubuntu-6891
[INFO] [launch]: Default logging verbosity is set to INFO
[INFO] [originbot_base-1]: process started with pid [6893]
[INFO] [static_transform_publisher-2]: process started with pid [6895]
[INFO] [static_transform_publisher-3]: process started with pid [6897]
[INFO] [static_transform_publisher-4]: process started with pid [6899]
[originbot_base-1] Loading parameters:
[originbot_base-1]              - port name: ttyS3
[originbot_base-1]              - correct factor vx: 0.8980
[originbot_base-1]              - correct factor vth: 0.8740
[originbot_base-1]              - auto stop on: 0
[originbot_base-1]              - use imu: 0
[static_transform_publisher-4] [INFO] [1688892599.398482288] [static_transform_publisher_wrXGY3d4cJPrfMMt]: Spinning until killed publishing transform from '/base_link' to '/imu_link'
[static_transform_publisher-2] [INFO] [1688892599.404346159] [static_transform_publisher_f8bfUI3IdvTPSv5L]: Spinning until killed publishing transform from '/base_footprint' to '/base_link'
[originbot_base-1] [INFO] [1688892599.417785811] [originbot_base]: originbot serial port opened
[originbot_base-1] [INFO] [1688892599.919219715] [originbot_base]: OriginBot Start, enjoy it.

```

### Keyboard Control Robot

Run the following command in another terminal to enable keyboard control:

tros foxy:
```bash
source /opt/tros/setup.bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard 
```
tros humble:
```bash
source /opt/tros/humble/setup.bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```

After successful execution, the following prompts will appear:

```bash
This node takes keypresses from the keyboard and publishes them
as Twist messages. It works best with a US keyboard layout.
---------------------------
Moving around:
   u    i    o
   j    k    l
   m    ,    .

For Holonomic mode (strafing), hold down the shift key:
---------------------------
   U    I    O
   J    K    L
   M    <    >

t : up (+z)
b : down (-z)

anything else : stop

q/z : increase/decrease max speeds by 10%
w/x : increase/decrease only linear speed by 10%
e/c : increase/decrease only angular speed by 10%

CTRL-C to quit

currently:      speed 0.5       turn 1.0
```

Control the robot's movement using the corresponding keys on the keyboard.

# Interface Description
## Topics

### Subscribed Topics

| Name               | Message Type                   | Description                                  |
| ------------------ | ------------------------------ | -------------------------------------------- |
| /cmd_vel           | geometry_msgs/msg/Twist        | Publish velocity commands to control the robot's movement |


### Published Topics

| Name               | Message Type                   | Description                                  |
| ------------------ | ------------------------------ | -------------------------------------------- |
| /originbot_status  | originbot_msgs/msg/OriginbotStatus  | Publish OriginBot robot status       |
| /odom              | nav_msgs/msg/Odometry           | Publish OriginBot odometry information       |
| /tf_static         | tf2_msgs/msg/TFMessage          | Publish OriginBot related coordinate information       |

## Parameters
| Parameter Name      | Type         | Description                         | Required | Default Value                                        |
| ------------------  | ------------- | ---------------------------------- | -------- | --------------------------- |
| auto_stop_on_arg    | bool          | Enable automatic stop function      | No       | false |
| use_imu_arg         | bool          | Enable IMU                          | No       | false |
| pub_odom_arg        | bool          | Enable publishing Odom topic        | No       | true |
| correct_factor_vx_arg  | float       | Linear velocity correction parameter | No       | 0.898 |
| correct_factor_vth_arg | float       | Angular velocity correction parameter | No       | 0.874 |


# FAQ

