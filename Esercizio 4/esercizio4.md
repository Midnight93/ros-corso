## Funzione Move
```python
def move(velocity_publisher, speed, distance, is_forward):
        #declare a Twist message to send velocity commands
        velocity_message = Twist()
        #get current location
        global x, y
        x0=x
        y0=y

        if (is_forward):
            velocity_message.linear.x =abs(speed)
        else:
        	velocity_message.linear.x =-abs(speed)

        distance_moved = 0.0
        loop_rate = rospy.Rate(10) # we publish the velocity at 10 Hz (10 times a second)    

        while True :
                rospy.loginfo("Turtlesim moves forwards")
                velocity_publisher.publish(velocity_message)

                loop_rate.sleep()

                distance_moved = abs(math.sqrt(((x-x0) ** 2) + ((y-y0) ** 2)))
                print  (distance_moved)
                print(x)
                if  not (distance_moved<distance):
                    rospy.loginfo("reached")
                    break

        #finally, stop the robot when the distance is moved
        velocity_message.linear.x =0
        velocity_publisher.publish(velocity_message)
```
## Funzione Rotate
```python
def rotate (velocity_publisher, angular_speed_degree, relative_angle_degree, clockwise):

    velocity_message = Twist()

    angular_speed=math.radians(abs(angular_speed_degree))

    if (clockwise):
        velocity_message.angular.z =-abs(angular_speed)
    else:
        velocity_message.angular.z =abs(angular_speed)

    angle_moved = 0.0
    loop_rate = rospy.Rate(10) # we publish the velocity at 10 Hz (10 times a second)    
    cmd_vel_topic='/turtle1/cmd_vel'
    velocity_publisher = rospy.Publisher(cmd_vel_topic, Twist, queue_size=10)

    t0 = rospy.Time.now().to_sec()

    while True :
        rospy.loginfo("Turtlesim rotates")
        velocity_publisher.publish(velocity_message)

        t1 = rospy.Time.now().to_sec()
        current_angle_degree = (t1-t0)*angular_speed_degree
        loop_rate.sleep()



        if  (current_angle_degree>relative_angle_degree):
            rospy.loginfo("reached")
            break

    #finally, stop the robot when the distance is moved
    velocity_message.angular.z =0
    velocity_publisher.publish(velocity_message)
```
## Funzione go_to_goal
```python
def go_to_goal(velocity_publisher, x_goal, y_goal):
    global x
    global y, yaw

    velocity_message = Twist()

    while (True):
        K_linear = 0.5
        distance = abs(math.sqrt(((x_goal-x) ** 2) + ((y_goal-y) ** 2)))

        linear_speed = distance * K_linear

        K_angular = 4.0
        desired_angle_goal = math.atan2(y_goal-y, x_goal-x)
        angular_speed = (desired_angle_goal-yaw)*K_angular

        velocity_message.linear.x = linear_speed
        velocity_message.angular.z = angular_speed

        velocity_publisher.publish(velocity_message)
        print ('x=', x, ', y=',y, ', distance to goal: ', distance)

        if (distance <0.01):
            break
```
## Funzione setDesiredOrientation
```python
def gridClean(publisher):

    desired_pose = Pose()
    desired_pose.x = 1
    desired_pose.y = 1
    desired_pose.theta = 0

    go_to_goal(publisher, 1,1)

    setDesiredOrientation(publisher, 30, math.radians(desired_pose.theta))

    for i in range(5):
        move(publisher, 2.0, 1.0, True)
        rotate(publisher, 20, 90, False)
        move(publisher, 2.0, 9.0, True)
        rotate(publisher, 20, 90, True)
        move(publisher, 2.0, 1.0, True)
        rotate(publisher, 20, 90, True)
        move(publisher, 2.0, 9.0, True)
        rotate(publisher, 20, 90, False)
    pass
```

## Funzione gridClean
```python
def gridClean(publisher):

    desired_pose = Pose()
    desired_pose.x = 1
    desired_pose.y = 1
    desired_pose.theta = 0

    go_to_goal(publisher, 1,1)

    setDesiredOrientation(publisher, 30, math.radians(desired_pose.theta))

    for i in range(5):
        move(publisher, 2.0, 1.0, True)
        rotate(publisher, 20, 90, False)
        move(publisher, 2.0, 9.0, True)
        rotate(publisher, 20, 90, True)
        move(publisher, 2.0, 1.0, True)
        rotate(publisher, 20, 90, True)
        move(publisher, 2.0, 9.0, True)
        rotate(publisher, 20, 90, False)
    pass
```
## Ros Launch

```bash
roslaunch [name_package] [name_file_launch]
```

Argomento | Link
------------ | -------------
ROS Launch| http://wiki.ros.org/roslaunch
ROS Launch Includes | http://wiki.ros.org/ROS/Tutorials/Roslaunch%20tips%20for%20larger%20projects
ROS Launch Params | http://wiki.ros.org/roslaunch/XML#Setting_parameters

### Esempio

```xml
<launch>
  <node name="turtlesim" pkg="turtlesim" type="turtlesim_node" />
  <node name="clean_node" pkg="ros_essentials_cpp" type="turtlesim_cleaner.py" output="screen" />
</launch>
```
## Ros Launch con i parametri

### Esempio con include

```xml
<launch>
  <group name="wg">
    <include file="$(find pr2_alpha)/$(env ROBOT).machine" />
    <include file="$(find 2dnav_pr2)/config/new_amcl_node.xml" />
    <include file="$(find 2dnav_pr2)/config/base_odom_teleop.xml" />
    <include file="$(find 2dnav_pr2)/config/lasers_and_filters.xml" />
    <include file="$(find 2dnav_pr2)/config/map_server.xml" />
    <include file="$(find 2dnav_pr2)/config/ground_plane.xml" />
    <!-- The navigation stack and associated parameters -->
    <include file="$(find 2dnav_pr2)/move_base/move_base.xml" />
  </group>
</launch>
```

### Esempio con parametri
```xml
<launch>
  <param name="somestring1" value="bar" />
  <!-- force to string instead of integer -->
  <param name="somestring2" value="10" type="str" />
  <param name="someinteger1" value="1" type="int" />
  <param name="someinteger2" value="2" />
  <param name="somefloat1" value="3.14159" type="double" />
  <param name="somefloat2" value="3.0" />
  <!-- you can set parameters in child namespaces -->
  <param name="wg/childparam" value="a child namespace parameter" />
  <!-- upload the contents of a file to the server -->
  <param name="configfile" textfile="$(find roslaunch)/example.xml" />
  <!-- upload the contents of a file as base64 binary to the server -->
  <param name="binaryfile" binfile="$(find roslaunch)/example.xml" />
</launch>
```
