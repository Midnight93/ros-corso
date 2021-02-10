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
