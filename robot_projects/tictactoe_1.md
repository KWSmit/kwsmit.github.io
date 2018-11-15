---
layout: robot
title: "Robots & more"
robot: "Tic Tac Toe (version 1)"
date: 2018-10-09
---

This is my first attempt to create a tic tac toe robot. A human user can play 
against the EV3 robot. The robot draws the lines and crosses, the human player 
has to put cirkels to the playfield. The design of the robot is based on the 
work of 
<a href="https://www.youtube.com/watch?v=x1Q8h7qegjk" target="_blank">Mike Koulouras</a>, 
with some minor adjustments. For the algorithm – to calculate the next move – 
I wanted to use the *minimax* algorithm. But in the end I used a 
more simple <a href="https://www.gliffy.com/publish/4867101/" taget="_blank">algorithm</a>.
I will implement minimax in the future (see version 2).

More information about the minimax algorithm can be found 
<a href="http://neverstopbuilding.com/minimax" target="_blank">here</a>.

<img src="/images/tictactoe_full.jpg" width="500">

The human player has to draw filled circles in the field. Reason for this is 
that otherwise the robot makes to many mistakes in seeing the difference 
between the moves of the human player or himself. Moves are scanned by the 
LEGO colorsensor in Ambient Light Intensity Mode. The difference in value 
between crosses and open circles is to small to let the robot determine the 
right moves. Lighting conditions also have influence on the sensor reading. 
This is still something to improve. When you watch the video of MIke Koulouras 
you see that is can be done…

<iframe width="560" height="315" src="https://www.youtube.com/embed/MIcjnmuTxCk" frameborder="0" allowfullscreen></iframe>

The program is written in *RobotC*, download code 
<a href="/downloads/TicTacToeEV3.zip" target="_blank">here</a>.
