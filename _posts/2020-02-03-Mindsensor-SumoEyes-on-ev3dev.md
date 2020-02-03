---
layout: post
title: "Robots & more"
subject: "Using Mindsensor's SumoEyes on ev3dev"
date: 2020-02-03
---

This blog will explain how to use the SumoEyes sensor from Mindsensors.com.
SumoEyes is a dual range, triple zone infrared obstacle detector for LEGO NXT
and EV3.

<img src="/images/sumo_eyes.png" width="458">

In ev3dev there isn't a driver for this sensor (yet), but there is still
an easy way to use it: by reading the output voltage of the sensor. Take
the following steps to do this:

- Connect the sensor to an input port on the EV3.
- Go to the `Device Browser` menu in Brickman and choose `Ports`.
- Select the port to which you connected the sensor.
- Set the mode of this port to `nxt-analog`.

In the Python code you can do it like this:

```python
# Mindsensor Sumo-eyes connected to port 1
in1 = LegoPort(INPUT_1)
in1.mode = 'nxt-analog'
sleep(0.5)
sumo = Sensor(INPUT_1)
```

Now you can read the voltage ouput with:

```python
sumo_value = sumo.value()
```

The value is an integer giving the voltage in mVolts, so devide by
1.000 to convert it to Volts.
The output voltage changes when the sensor detects an object:

- `sumo_value > 4V` means nothing is detected
- `sumo_value > 3V` means something is detected right in front of the sensor
- `sumo_value > 2V` means something is detected on the right side of the sensor
- `sumo_value > 1V` means something is detected on the left side of the sensor

Following sample code runs a robot with two LargeMoters and it uses the sensor
measurements to avoid obstacles:

```python
#!/usr/bin/env python3
from sys import stderr
import math
import random
from ev3dev2.sensor import INPUT_1, Sensor
from ev3dev2.motor import OUTPUT_A, OUTPUT_D, MoveSteering
from ev3dev2.port import LegoPort
from time import sleep

def sign():
    """ Return randomly -1 or 1."""
    return random.randrange(-1, 2, 2)

SUMO_FRONT = 1
SUMO_RIGHT = 2
SUMO_LEFT = 3
SUMO_NONE = 4

# Mindsensor Sumo-eyes connected to port 1
in1 = LegoPort(INPUT_1)
in1.mode = 'nxt-analog'
sleep(0.5)
sumo = Sensor(INPUT_1)

# Motors
move_steering = MoveSteering(OUTPUT_A, OUTPUT_D)

while True:
    # Read output voltage of SumoEye sensor
    # Divide by 1000 and convert to int (so you get a
    # value between 0 and 4, see constants above)
    sumo_value = int(sumo.value()/1000)
    if sumo_value == SUMO_NONE:
        # Road ahead is clear, keep driving forward
        move_steering.on(0, 30)
    elif sumo_value == SUMO_FRONT:
        # Road in front is blocked, change direction (random)
        move_steering.on(sign()*100, 30)
    elif sumo_value == SUMO_RIGHT:
        # Road on the right is blocked, steer to the left
        move_steering.on(50, 30)
    elif sumo_value == SUMO_LEFT:
        # Road on the left is blocked, steer to the right
        move_steering.on(-50, 30)
    sleep(0.1)
```

There is one drawback: the sensor has two possible modes, a 
`short-range` and a `long-range` mode. In the way we are using this
sensor here, it is not possible to set the mode.

Useful links:

- Information about SumoEyes sensor (<a href="http://www.mindsensors.com/ev3-and-nxt/28-dual-range-triple-zone-infrared-obstacle-detector-for-nxt-or-ev3" target="_blank">Website mindsensors.com</a>).
