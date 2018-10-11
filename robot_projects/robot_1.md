---
layout: robot
title: "Robot1"
date: 2018-10-09
---

Here comes an article about *Robot 1*.

```python
from ev3dev.ev3 import *
pixy = Sensor(address=INPUT_1)
assert pixy.connected, "Error while connecting Pixy camera to port1"
```

> This is a block quote.
> Second line.