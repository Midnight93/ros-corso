# ros-corso
ROS codice esercizi


![Ros](media/image1.jpg)


## Installazione ROS


## Esercizio 1

### Talker.py

```python

import rospy
from std_msgs.msg import String

def chatter_callback(message):
    rospy.loginfo(rospy.get_caller_id() + "I heard %s", message.data)

def listener():
    rospy.init_node('listener', anonymous=True)

    rospy.Subscriber('chatter', String, chatter_callback)

    rospy.spin()

if __name__ = '__main__'
    listener()


```
### Listener.py

```python

import rospy
from std_msgs.msg import String

#Creazione del topic con la classe Publisher
pub = rospy.Publisher('chatter', String, queue_size=10) #Nome Topic, Tipologia messaggio, Buffer

#Inizializiamo il nodo
#Nome del nodo, Anonymus significa che il node è unico
rospy.init_node('talker', anonymous=True)

#il numero 1 indicata la frequenza espressa in Hz
rate = rospy.Rate(1)

#Contatore
i=0

while not rospy.is_shutdown():
    hello_str = "hello world %s" % i
    rospy.loginfo(hello_str)
    pub.publish(hello_str)
    rate.sleep()
    i=i+1
```

## Esercizio 2

- IoT_message

```python
int32 id
string name
float32 temperature
float32 humidity
```
- Configurazione del CMakeLists.txt

- Creazione del subscriber e publisher

### iot_sensor_publisher_talker.py

```python
#!/usr/bin/env python
# license removed for brevity
import rospy
from ros_essentials_cpp.msg import IoTSensor
import random

#create a new publisher. we specify the topic name, then type of message then the queue size
pub = rospy.Publisher('iot_sensor_topic', IoTSensor, queue_size=10)

#we need to initialize the node
rospy.init_node('iot_sensor_publisher_node', anonymous=True)

#set the loop rate
rate = rospy.Rate(1) # 1hz
#keep publishing until a Ctrl-C is pressed
i = 0
while not rospy.is_shutdown():
    iot_sensor = IoTSensor()
    iot_sensor.id = 1
    iot_sensor.name="iot_parking_01"
    iot_sensor.temperature = 24.33 + (random.random()*2)
    iot_sensor.humidity = 33.41+ (random.random()*2)
    rospy.loginfo("I publish:")
    rospy.loginfo(iot_sensor)
    pub.publish(iot_sensor)
    rate.sleep()
    i=i+1
```
### iot_sensor_publisher_talker.py

```python
#!/usr/bin/env python
# license removed for brevity
import rospy
from ros_essentials_cpp.msg import IoTSensor
import random

#create a new publisher. we specify the topic name, then type of message then the queue size
pub = rospy.Publisher('iot_sensor_topic', IoTSensor, queue_size=10)

#we need to initialize the node
rospy.init_node('iot_sensor_publisher_node', anonymous=True)

#set the loop rate
rate = rospy.Rate(1) # 1hz
#keep publishing until a Ctrl-C is pressed
i = 0
while not rospy.is_shutdown():
    iot_sensor = IoTSensor()
    iot_sensor.id = 1
    iot_sensor.name="iot_parking_01"
    iot_sensor.temperature = 24.33 + (random.random()*2)
    iot_sensor.humidity = 33.41+ (random.random()*2)
    rospy.loginfo("I publish:")
    rospy.loginfo(iot_sensor)
    pub.publish(iot_sensor)
    rate.sleep()
    i=i+1
```

## Esercizio 3

#### ROS Services

##### Service Node
