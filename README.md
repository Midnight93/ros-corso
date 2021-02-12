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

$ sudo apt-get update
$ sudo apt-get upgrade

```

```bash
$ cd
$ cd catkin_ws/src
$ git clone https://github.com/ROBOTIS-GIT/turtlebot3.git
$ cd
$ cd catkin_ws/ && catkin_make
```

### Installazione del simulatore del TurtleBot 3

```bash
$ cd ~/catkin_ws/src
$ git clone https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
$ cd ~/catkin_ws && catkin_make
```
### Setting del file .bashrc 

```bash

$ cd 
$ gedit .bashrc

```

```bash

# ~/.bashrc: executed by bash(1) for non-login shells.
# see /usr/share/doc/bash/examples/startup-files (in the package bash-doc)
# for examples

# If not running interactively, don't do anything
case $- in
    *i*) ;;
      *) return;;
esac

# don't put duplicate lines or lines starting with space in the history.
# See bash(1) for more options
HISTCONTROL=ignoreboth

# append to the history file, don't overwrite it
shopt -s histappend

# for setting history length see HISTSIZE and HISTFILESIZE in bash(1)
HISTSIZE=1000
HISTFILESIZE=2000

# check the window size after each command and, if necessary,
# update the values of LINES and COLUMNS.
shopt -s checkwinsize

# If set, the pattern "**" used in a pathname expansion context will
# match all files and zero or more directories and subdirectories.
#shopt -s globstar

# make less more friendly for non-text input files, see lesspipe(1)
[ -x /usr/bin/lesspipe ] && eval "$(SHELL=/bin/sh lesspipe)"

# set variable identifying the chroot you work in (used in the prompt below)
if [ -z "${debian_chroot:-}" ] && [ -r /etc/debian_chroot ]; then
    debian_chroot=$(cat /etc/debian_chroot)
fi

# set a fancy prompt (non-color, unless we know we "want" color)
case "$TERM" in
    xterm-color|*-256color) color_prompt=yes;;
esac

# uncomment for a colored prompt, if the terminal has the capability; turned
# off by default to not distract the user: the focus in a terminal window
# should be on the output of commands, not on the prompt
#force_color_prompt=yes

if [ -n "$force_color_prompt" ]; then
    if [ -x /usr/bin/tput ] && tput setaf 1 >&/dev/null; then
	# We have color support; assume it's compliant with Ecma-48
	# (ISO/IEC-6429). (Lack of such support is extremely rare, and such
	# a case would tend to support setf rather than setaf.)
	color_prompt=yes
    else
	color_prompt=
    fi
fi

if [ "$color_prompt" = yes ]; then
    PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
else
    PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '
fi
unset color_prompt force_color_prompt

# If this is an xterm set the title to user@host:dir
case "$TERM" in
xterm*|rxvt*)
    PS1="\[\e]0;${debian_chroot:+($debian_chroot)}\u@\h: \w\a\]$PS1"
    ;;
*)
    ;;
esac

# enable color support of ls and also add handy aliases
if [ -x /usr/bin/dircolors ]; then
    test -r ~/.dircolors && eval "$(dircolors -b ~/.dircolors)" || eval "$(dircolors -b)"
    alias ls='ls --color=auto'
    #alias dir='dir --color=auto'
    #alias vdir='vdir --color=auto'

    alias grep='grep --color=auto'
    alias fgrep='fgrep --color=auto'
    alias egrep='egrep --color=auto'
fi

# colored GCC warnings and errors
#export GCC_COLORS='error=01;31:warning=01;35:note=01;36:caret=01;32:locus=01:quote=01'

# some more ls aliases
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'




# Add an "alert" alias for long running commands.  Use like so:
#   sleep 10; alert
alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'

# Alias definitions.
# You may want to put all your additions into a separate file like
# ~/.bash_aliases, instead of adding them here directly.
# See /usr/share/doc/bash-doc/examples in the bash-doc package.

if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi

# enable programmable completion features (you don't need to enable
# this, if it's already enabled in /etc/bash.bashrc and /etc/profile
# sources /etc/bash.bashrc).
if ! shopt -oq posix; then
  if [ -f /usr/share/bash-completion/bash_completion ]; then
    . /usr/share/bash-completion/bash_completion
  elif [ -f /etc/bash_completion ]; then
    . /etc/bash_completion
  fi
fi

alias burger='export TURTLEBOT3_MODEL=burger'
alias waffle='export TURTLEBOT3_MODEL=waffle'
alias tb3fake='roslaunch turtlebot3_fake turtlebot3_fake.launch'
alias tb3teleop='roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch'
alias tb3='roslaunch turtlebot3_gazebo turtlebot3_empty_world.launch'
alias tb3maze='roslaunch turtlebot3_gazebo turtlebot3_world.launch'
alias tb3house='roslaunch turtlebot3_gazebo turtlebot3_house.launch'
source /opt/ros/noetic/setup.bash
source /home/ros/catkin_ws/devel/setup.bash
export TURTLEBOT3_MODEL=waffle
export SVGA_VGPU10=0

```
### Turtlebot3 all'interno di un mondo vuoto ( Empty World Environment )

```bash

$ roslaunch turtlebot3_gazebo turtle3_empty_world.launch

```

### Turtlebot3 World Enviroment

```bash

$ roslaunch turtlebot3_gazebo turtlebo3_world.launch

```

### Turtlebot3 House Environment 

```bash

$ roslaunch turtlebot3_gazebo turtlebo3_house.launch

```

### Turtlebo3 RVIZ

```bash

roslaunch turtlebot3_gazebo turtlebot3_gazebo_rviz.launch

```

### Turtlebot3 SLAM for Map Building


```bash

$ roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping

$ roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch

```
