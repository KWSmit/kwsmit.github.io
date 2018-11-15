---
layout: post
title: "Robots & more"
subject: "Sending and retreiving messages with MQTT"
date: 2017-01-02
---

<a href="https://en.wikipedia.org/wiki/MQTT" target="_blank">MQTT</a> 
(Message Queue Telemetry Transport) is an ISO standard (ISO/IEC PRF 20922) 
publish-subscribe based “light weight” messaging protocol for use on top 
of the TCP/IP protocol. It is designed for connections with remote locations 
where a “small code footprint” is required or the network bandwidth is limited.
<br><br>It’s very easy to use the MQTT protocol to exchange small messages between 
several EV3 devices. An explanation how to use it with python and ev3dev can 
be found on the website of ev3dev.org. It’s recently updated for python3.
<br><br>I created a simple testapplication where one EV3-1 is controlled by the 
LEGO remote control for EV3. This robot sends messages about it’s movements 
to EV3-2. This way EV3-2 mimics the movements of EV3-1, see video below.

<iframe width="560" height="315" src="https://www.youtube.com/embed/oIzKvRp9guU" frameborder="0" allowfullscreen></iframe>
<br>
