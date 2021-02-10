# Corso Ros

![Ros](media/image1.jpg)

# Installazione Ros

### Setup sources.list
```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```

### Adding Key
```
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
```

### Update package list
```
sudo apt-get update
```

### Installing ROS Kinetic Full Desktop Version
```
sudo apt-get install ros-kinetic-desktop-full
```

### Initialize Ros Dependencies
```
sudo rosdep init
```
```
rosdep update
```

### Setting up ROS Environment
```
printf "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc
```
```
source ~/.bashrc
```

### Installing Python Packages for ROS
```
sudo apt-get install python-rosinstall
```
```
sudo apt install python-catkin-tools
```

### Other Important ROS Packages
```
sudo apt-get install ros-kinetic-tf-*
```
```
sudo apt-get install ros-kinetic-pcl-msgs ros-kinetic-mav-msgs ros-kinetic-mavros ros-kinetic-octomap-* ros-kinetic-geographic-msgs libgeographic-dev
```

### Creating Catkin Workspace
```
mkdir catkin_ws
```
```
cd catkin_ws
```
```
mkdir -p src
```
```
cd src
```
```
catkin_init_workspace
```
```
printf "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
```
```
cd ~/catkin_ws
```
```
catkin_make
```
```
source ~/catkin_ws/devel/setup.bash
```

# Manda messaggio topic TurtleSim
```python
rostopic pub -r 1 /turtle1/cmd_vel geometry_msg/Twist [TAB] [TAB]
```

## Tabella Arcotangente

![arco](media/Immagine.jpg)


## Ros Networking

Argomento | Link
------------ | -------------
ROS NetworkSetup | http://wiki.ros.org/ROS/NetworkSetup
Running ROS across multiple REMOTE machines | http://wiki.ros.org/ROS/Tutorials/MultipleRemoteMachines

## Ros Launch

```bash
roslaunch [name_package] [name_file_launch]
```

Argomento | Link
------------ | -------------
ROS Launch| http://wiki.ros.org/roslaunch
ROS Launch Includes | http://wiki.ros.org/ROS/Tutorials/Roslaunch%20tips%20for%20larger%20projects
ROS Launch Params | http://wiki.ros.org/roslaunch/XML#Setting_parameters

### Turtlebot 3

![Turtlebot3](media/turtlebot3.png)

### Installazione

```bash
$ cd
$ cd catkin_ws/src
$ git clone https://github.com/ROBOTIS-GIT/turtlebot3.git
$ cd
$ cd catkin_ws/ && catkin_make
```
