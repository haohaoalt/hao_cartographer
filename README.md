<!--
 * @Author: zhanghao
 * @Date: 2022-07-12 20:07:57
 * @LastEditTime: 2022-08-10 12:45:55
 * @FilePath: /hao_cartographer/README.md
 * @Description: 
-->
# hao_cartographer
my cartographer repository

> https://google-cartographer-ros.readthedocs.io/en/latest/index.html
## cartographer ros compiling
- 1. It is confirmed to be working on systems that meet the following requirements:
  - 64-bit, modern CPU (e.g. 3rd generation i7)
  - 16 GB RAM
  - Ubuntu 18.04 (Bionic), 20.04 (Focal), 22.04 (Jammy)
  - gcc version 6.3.0, 7.5.0, 9.3.0, 11.2.0

- 2. The following ROS distributions are currently supported:
Kinetic
Melodic
Noetic

- 3. building & installation
On Ubuntu Focal with ROS Noetic use these commands to install the above tools:
```
sudo apt-get update
sudo apt-get install -y python3-wstool python3-rosdep ninja-build stow
```
On older distributions:
```
sudo apt-get update
sudo apt-get install -y python-wstool python-rosdep ninja-build stow
```
After the tools are installed, create a new cartographer_ros workspace in ‘catkin_ws’.
```
wstool init src
wstool merge -t src https://raw.githubusercontent.com/cartographer-project/cartographer_ros/master/cartographer_ros.rosinstall
wstool update -t src
```
Now you need to install cartographer_ros’ dependencies. First, we use rosdep to install the required packages. The command ‘sudo rosdep init’ will print an error if you have already executed it since installing ROS. This error can be ignored.

```
sudo rosdep init
rosdep update
rosdep install --from-paths src --ignore-src --rosdistro melodic -r -y

```
Cartographer uses the abseil-cpp library that needs to be manually installed using this script:

src/cartographer/scripts/install_abseil.sh
Due to conflicting versions you might need to uninstall the ROS abseil-cpp using
```
sudo apt-get remove ros-${ROS_DISTRO}-abseil-cpp
```
```
cd src
cd cartographer
cd scripts
chmod +x install_abseil.sh
./install_abseil.sh
```

Build and install.
```
cd ~/hao_cartographer
catkin_make_isolated --install --use-ninja
```


## 2d建图指令

`roslaunch cartographer_ros hao_2d.launch`

## 保存2d轨迹,并生成ros格式的地图

`./hao_2d_finish.sh`

## 纯定位模式

`roslaunch cartographer_ros hao_2d_localization.launch`

## 使用asset生成ros格式的2d栅格地图

`roslaunch cartographer_ros assets_writer_2d.launch`

## landmark使用示例

`roslaunch cartographer_ros landmark_mir_100.launch`






