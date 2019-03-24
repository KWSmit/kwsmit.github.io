---
layout: post
title: "Robots & more"
subject: "Working with RPyC"
date: 2017-01-13
---

RPyC (pronounced as are-pie-see), or Remote Python Call, is a transparent 
python library for symmetrical remote procedure calls, clustering and 
distributed-computing. RPyC makes use of object-proxying, a technique 
that employs python’s dynamic nature, to overcome the physical boundaries 
between processes and computers, so that remote objects can be manipulated 
as if they were local 
(source: <a href="https://python-ev3dev.readthedocs.io/en/latest/rpyc.html" target="_blank">
ev3dev Python language doc)</a>.

Sounds interesting, so I did some exploring into this subject. 
Installation on EV3 and PC is straightforward and well documented on the 
ev3dev Python language doc. On my Windows PC I installed RPyC from the 
command window using pip.

I found out there are two ways to use RPyC:

- Using services and <a href="https://rpyc.readthedocs.io/en/latest/tutorial/tut3.html" target="_blank">
New style RPyC</a>.
- Using the <a href="https://rpyc.readthedocs.io/en/latest/tutorial/tut1.html" target="_blank">
classic server</a>.

## Using New style RPyC

A clear explanation can be found on the given link above. Her I will just 
show you some simple code snippets to get it working on your own EV3. These 
examples also make use of ev3dev, my preferred programming environment 
for the EV3.

### On the EV3

```python
import rpyc
from rpyc.utils.server import ThreadedServer
from ev3dev.ev3 import *

class MyService(rpyc.Service):
    def exposed_speak_message(self, msg):
        Sound.speak(msg)

if __name__ == '__main__':
    s = ThreadedServer(MyService, port=18812)
    s.start()
```

First import the module *rpyc* and *ThreadedServer* and the ev3dev module 
(I’ll use the Sound class from ev3dev in this script). Next define 
a class (in this case *MyService*), just like you define any other 
class in Python. Unlike regular classes, however, you can choose which 
attributes will be exposed to the other party: if the name starts with 
*exposed_*, the attribute will be remotely accessible, otherwise it is 
only locally accessible. In my example above, clients will be able to 
call *speak_message*. Parameters of *speak_message* are *self* 
(because it is a function belonging to class *MyService*) and *msg*, 
the text I want EV3 to speak. In the function I use the speak function 
of the Sound class to make EV3 say the message.

To expose service *speak_message* to the world, you will need to start 
a server. There are many ways to do that, but the simplest is 
by starting a *ThreadedServer*.

Start this script and let it run on the EV3 before starting the 
script on your PC:

```python
robot@ev3dev:~$ python3 rpyc_test.py
```

### On the PC

```python
import rpyc

conn = rpyc.connect('$$$.$$$.$.$$', port=18812)
conn.root.speak_message('The answer is 42')
```

First import the RPyC library. Make RPyC-connection by giving the 
ip-address of the EV3 and defining the portnumber (must be the same as 
defined in the script on your EV3). Now you can call the desired service, 
in this case speak_message. To the PC, this service is exposed as the 
root object of the connection: *conn.root*.

This example makes the EV3 say the famous words: “The answer is 42”.

## Using the classic server

### On the EV3

First write the script *rpyc_classic_ev3.py*:

```python
#!/usr/bin/env python3
from ev3dev.ev3 import *

def speak_message(msg):
    Sound.speak(msg)
```

Next write the script *rpyc_server.sh*:

```python
#!/bin/bash
python3 `which rpyc_classic.py`
```

Start this serverscript on the EV3:

```python
robot@ev3dev:~$ ./rpyc_server.sh
```

When the server is running you’ll see a message like this:

```python
INFO:SLAVE/18812:server started on [0.0.0.0]:18812
```

Now you can turn to your PC.

### On the PC

```python
import rpyc

conn = rpyc.classic.connect('$$$.$$$.$.$$')
conn.modules.sys.path.append('/home/robot')
e = conn.modules.rpyc_classic_ev3
e.speak_message('Listen carefully, I will only tell this once')
```

Use *rpyc.classic.connect* to connect to the EV3 ($$$.$$$.$.$$ is the 
ip-address of your EV3). To find the desired module on the EV3 you need 
to add the path to de directory containing the file. Next create an object 
to the module on the EV3 (in this case *rpyc_classic_ev3.py*) and call the 
function *speak_message* and your EV3 starts speaking.
