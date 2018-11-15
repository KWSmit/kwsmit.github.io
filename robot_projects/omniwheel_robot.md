---
layout: robot
title: "Robots & more"
robot: "Omniwheel robot"
date: 2014-10-09
---

This is a robot using omniwheels. Normal wheels can only turn in one 
direction, but omniwheels are able to drive in all directions due to small 
rollers. These rollers have their axis perpendular on de main axis of the 
wheel. In this robot I used omniwheels by *Nexus Robot*.

<img src="/images/omniwheel.jpg" width="183">

Xander Soldaat 
(<a href="http://botbench.com/blog/2014/05/11/omniwheel-article-in-dt-practice/" target="_blank">Bot Bench</a>) 
gives a good explanation in his article about omniwheels. I used his 
article to built this robot. The robot is programmed by using the MonoBrick 
Communication Library. When starting the application on your computer the 
userinterface shows several buttons. 

<img src="/images/wfa-omniwheel-ui.png" width="310">

Controlling the robot is done by these buttons. Ev3 needs to be connected by 
Bluetooth. The Bluetooth port (e.g. com4) must be given in the ini-file which 
resides in the same directory as the executable. By pressing ‘Forward’ the 
robot goes straight forward. When pressing ‘Go Left’ the robot moves to the 
left but keeps the same orientation. In other words, it slides to the left. 
When pressing one of the ‘Turn’ buttons, the robot turns around on its place, 
thus its orientation changes. By using the sliders the driving speed or the 
speed in which it turns can be adjusted (range 0 to 100).
The ‘Start Searching’ button makes EV3 turn around to find the beacon. When 
found, the robots starts driving to the beacon. As you can see in the video, 
some adjustment needs to be done here: of course it has to stop in front 
of the beacon.

<iframe width="560" height="315" src="https://www.youtube.com/embed/Dl3Li54XnsU" frameborder="0" allowfullscreen></iframe>
<br>
<p>Download the LEGO Digital Designer file <a href="/downloads/LDD_OmniWheelWFA.zip" download>here</a>.</p>