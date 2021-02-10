## Esercizio 3

#### ROS Services

##### Service Node

#### Open the Turtlesim simulator

```
roscsore
```

```
rosrun turtlesim turtlesim_node
```

Display the list of services
```
rosservice list
```
What is the command that shows the information of the service /reset
```
rosservice info /reset
```
Write the result of the execution of the command for the service /reset
```
Node: /turtlesim

URI: rosrpc://ace:xxx

Type: std_srvs/Empty
```
Args:

What is the command that shows the information of the service /kill
```
rosservice info /kill
```
Write the result of the execution of the command for the service /kill
```
Node: /turtlesim

URI: rosrpc://ace:xx

Type: turtlesim/Kill

Args: name
```


What is the command that shows the content of message turtlesim/Kill of the /kill service?
```
rosservice info /kill
```
Spaw one additional turtle called tsim1. Write the command.
```
rosservice call /spawn 7 7  0.55 tsim1   
```
use the service kill to kill tsim1.Write the command.  
```
rosservice call /kill tsim1
```
use the service reset to reset all the simulation. Write the command.
```
rosservice call /reset tsim1
```

## Server & Client

### Server

- server.py

```python

#!/usr/bin/env python

from ros_essentials_cpp.srv import AddTwoInts
from ros_essentials_cpp.srv import AddTwoIntsRequest
from ros_essentials_cpp.srv import AddTwoIntsResponse

import rospy

def handle_add_two_ints(req):
    print "Returning [%s + %s = %s]"%(req.a, req.b, (req.a + req.b))
    return AddTwoIntsResponse(req.a + req.b)

def add_two_ints_server():
    rospy.init_node('add_two_ints_server')
    s = rospy.Service('add_two_ints', AddTwoInts, handle_add_two_ints)
    print "Ready to add two ints."
    rospy.spin()

if __name__ == "__main__":
    add_two_ints_server()

```
### Client

- client.py

```python

#!/usr/bin/env python

import sys
import rospy
from ros_essentials_cpp.srv import AddTwoInts
from ros_essentials_cpp.srv import AddTwoIntsRequest
from ros_essentials_cpp.srv import AddTwoIntsResponse

def add_two_ints_client(x, y):
    rospy.wait_for_service('add_two_ints')
    try:
        add_two_ints = rospy.ServiceProxy('add_two_ints', AddTwoInts)
        resp1 = add_two_ints(x, y)
        return resp1.sum
    except rospy.ServiceException, e:
        print "Service call failed: %s"%e

def usage():
    return "%s [x y]"%sys.argv[0]

if __name__ == "__main__":
    if len(sys.argv) == 3:
        x = int(sys.argv[1])
        y = int(sys.argv[2])
    else:
        print usage()
        sys.exit(1)
    print "Requesting %s+%s"%(x, y)
    s = add_two_ints_client(x, y)
    print "%s + %s = %s"%(x, y, s)

```
