# 功能介绍

OriginBot是一款智能机器人开源套件，更是一个社区共建的开源项目，旨在让每一位参与者享受机器人开发的乐趣。该项目是OriginBot机器人最小功能系统，该最小系统可接受/cmd_vel指令控制机器人运动并反馈/Odom信息。该系统包含以下三个功能包：

- originbot_base：机器人底盘驱动
- originbot_driver：机器人串口驱动包
- originbot_msgs： OriginBot自定义通信接口

# 物料清单

| 机器人名称          | 生产厂家 | 参考链接                                                     |
| :------------------ | -------- | ------------------------------------------------------------ |
| OriginBot智能机器人 | 古月居   | [购买链接](https://www.originbot.org/)                       |
| RDK X3 Robot        | 多厂家 | [购买链接](https://developer.horizon.ai/sunrise) |

# 使用方法

## 准备工作

参考机器人官网的[使用指引](https://www.originbot.org/guide/quick_guide/)，完成机器人的硬件组装。

## 安装 

点击[NodeHub OriginBot项目](http://it-dev.horizon.ai/nodehubDetail/170117036053371431)右上角快速部署，通过终端或者VNC连接机器人，复制如下命令在RDK的系统上运行，完成人OriginBot机器人最小系统安装。

```bash
sudo apt update
sudo apt install -y tros-originbot-base tros-serial tros-originbot-msgs
```



## 运行

### 启动机器人

在终端中输入：

```bash
source /opt/tros/setup.bash
ros2 launch originbot_base robot.launch.py 
```
运行成功后可看到如下提示
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

### 键盘控制机器人

在另一个终端中运行如下指令打开键盘控制功能：

```bash
source /opt/tros/setup.bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard 
```
运行成功后出现以下提示
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
根据提示即可适用键盘控制机器人运动。

# 接口说明
## 话题

### 订阅话题

| 名称                          | 消息类型                                                     | 说明                                                   |
| ----------------------------- | ------------------------------------------------------------ | ------------------------------------------------------ |
| /cmd_vel                      | geometry_msgs/msg/Twist                                      | 发布控制机器人移动的速度指令                           |


### 发布话题

| 名称                          | 消息类型                                                     | 说明                                                   |
| ----------------------------- | ------------------------------------------------------------ | ------------------------------------------------------ |
| /originbot_status             |  originbot_msgs/msg/OriginbotStatus                          | 发布OriginBot机器人状态                           |
| /odom                         |  nav_msgs/msg/Odometry                                       | 发布OriginBot里程计信息                           |
| /tf_static                    |  tf2_msgs/msg/TFMessage                                      | 发布OriginBot相关坐标系信息                           |

## 参数
| 参数名                | 类型        | 解释                                 | 是否必须 | 默认值                                               |
| --------------------- | ----------- | ---------------------------------- | -------- | --------------------------- |
| auto_stop_on_arg      | bool    |     是否使能自动停止功能                 | 否       | false |
| use_imu_arg      | bool    |     是否使能IMU                 | 否       | false |
| pub_odom_arg      | bool    |     是否使能发布Odom话题                | 否       | true |
| correct_factor_vx_arg      | float    |  线速度校正参数                | 否       | 0.898 |
| correct_factor_vth_arg      | float    |  角速度校正参数                | 否       | 0.874 |


# 常见问题


