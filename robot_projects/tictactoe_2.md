---
layout: robot
title: "Robots & more"
robot: "PiStorms tic tac toe robot"
date: 2018-12-20
---

This is my second tic tac toe robot, a lot more sophisticated than 
my <a href="/robot_projects/tictactoe_1.html" target="_blank">first</a> one. 
For this one I used the power of a Raspberry Pi 3B by 
using the PiStorms v2 from mindsensors.com.

<img src="/images/KSmTicTacToePS1.jpg" width="520">

The program is written in Python on the ev3dev operating system. You'll 
find the code on 
<a href="https://github.com/KWSmit/KSmEV3TicTacToe--PiStorms-version-" target="_blank">
Github</a>.

For calculating the computer's moves I used the 
<a href="http://neverstopbuilding.com/minimax" target="_blank">Minimax</a>. 
This way the computer will always win or the game ends in a draw. Of course, 
this way it's no fun to play with, but if you like you can change the algorithm 
in such way that the computer does not always pick the best move out of all 
possibilities. You'll find many suggestions for this on the internet.

Of course the computer knows where it puts its own moves. To determine the 
moves of the human player I use a picamera. This camera takes a picture when 
the human player presses the touchsensor. Then the program uses OpenCV to 
detect the circles the human player drawed. Now it can use the Minimax 
algorithm to calculate the best move.

### Video

<iframe width="560" height="315" src="https://www.youtube.com/embed/VAQ4zRkutP0" frameborder="0" allowfullscreen></iframe>

### Photos

I didn't make any building instructions, but when you look at the pictures 
below, I'm sure you can build your own tic tac toe machine. Be sure to 
adust the settings for all LEGO motors and sensors (ports, speed_sp, 
position_sp, etc.) and for the picamera.

Overview<br>
<img src="/images/IMG_3442.jpg" width="500"><br>
<br>
Picamera<br>
<img src="/images/IMG_3447.jpg" width="500"><br>
<br>
Turntable (bottom view)<br>
<img src="/images/IMG_3438.jpg" width="500"><br>
<img src="/images/IMG_3439.jpg" width="500"><br>
<img src="/images/IMG_3448.jpg" width="500"><br>
<br>
Pen mechanism<br>
<img src="/images/IMG_3441.jpg" width="500"><br>
<img src="/images/IMG_3449.jpg" width="500"><br>
<img src="/images/IMG_3450.jpg" width="500"><br>
