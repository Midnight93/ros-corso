# Corso Ros

![Ros](media/image1.jpg)

# Installazione Ros

Argomento | Link | Compatibilità
------------ | ------------- | -------------
ROS Melodic | http://wiki.ros.org/melodic | Ubuntu 18.04 LTS
ROS Kinetic | http://wiki.ros.org/kinetic | Ubuntu 16.04 LTS
ROS Noetic  | http://wiki.ros.org/noetic  | Ubuntu 20.04


### Setup sources.list
```bash
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```

### Adding Key
```bash
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
```

### Update package list
```bash
sudo apt-get update
```

### Installing ROS Kinetic Full Desktop Version
```bash
sudo apt-get install ros-kinetic-desktop-full
```

### Initialize Ros Dependencies
```bash
sudo rosdep init
```
```bash
rosdep update
```

### Setting up ROS Environment
```bash
printf "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc
```
```bash
source ~/.bashrc
```

### Installing Python Packages for ROS
```bash
sudo apt-get install python-rosinstall
```
```bash
sudo apt install python-catkin-tools
```

### Other Important ROS Packages
```bash
sudo apt-get install ros-kinetic-tf-*
```
```bash
sudo apt-get install ros-kinetic-pcl-msgs ros-kinetic-mav-msgs ros-kinetic-mavros ros-kinetic-octomap-* ros-kinetic-geographic-msgs libgeographic-dev
```

### Creating Catkin Workspace
```bash
mkdir catkin_ws
```
```bash
cd catkin_ws
```
```bash
mkdir -p src
```
```bash
cd src
```
```bash
catkin_init_workspace
```
```bash
printf "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
```
```bash
cd ~/catkin_ws
```
```bash
catkin_make
```
```bash
source ~/catkin_ws/devel/setup.bash
```

# Creazione di un package

Argomento | Link
------------ | -------------
Creating a ROS Package | http://wiki.ros.org/ROS/Tutorials/CreatingPackage
Building a ROS Package| http://wiki.ros.org/ROS/Tutorials/BuildingPackages

# ROS Nodes

Argomento | Link
------------ | -------------
Understanding ROS Nodes | http://wiki.ros.org/ROS/Tutorials/UnderstandingNodes
rosnode| http://wiki.ros.org/rosnode

# ROS Topic

Argomento | Link
------------ | -------------
Understanding ROS Topics | http://wiki.ros.org/it/ROS/Tutorials/UnderstandingTopics
rostopic|http://wiki.ros.org/rostopic 

# ROS Message 

Argomento | Link
------------ | -------------
Creating a ROS msg and srv | http://wiki.ros.org/ROS/Tutorials/CreatingMsgAndSrv
rosmsg |http://wiki.ros.org/rosmsg 

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
