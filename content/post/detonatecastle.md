---
title:       "Detonate a castle in Minecraft"
subtitle:    ""
description: ""
date:        2021-02-15
author:      "Pawel Wasilewski"
image:       ""
tags:        ["Minecraft", "Python"]
categories:  ["Tutorials"]
---

TNT is one of the blocks most favourited by the Minecraft players and we are going to mess with it today. In our game, Steve will detonate the entrance to the castle after standing on the coloured brick.

{{<figure src="/castle/First1.png">}}

### Step 1

We start with building a simple castle. The constants X, Y and Z should reflect the coordinates in your world where you would like to stand to trigger the detonation. The castle will be built relative to these coordinates.

In this step, you will also write the function responsible for setting up a nice, flat piece of land and building a castle on it.

{{<figure src="/castle/1.png">}}

### Step 2

The first function will encapsulate all the building involved in the creation of the escape room. It will also teleport the player inside the room.

{{<figure src="/castle/2.png">}}

### Step 3

To build the crenellations, we will need to remove every second block on the top rows of our walls. Loops are a good way to code repeatable actions and we will use them here. The first loop will iterate every second value of the X coordinate ( note that the last parameter of the range() function is used to define the size of the step). Inside the loop body, a line of AIR blocks is being created that spans across the width of the castle. With this trick, we are modifying two walls at the same time! The second loop does the same job but it tackles the remaining two walls by iterating on the Z coordinate.

Please add lines 16 - 20 to your code.   

{{<figure src="/castle/3.png">}}

### Step 4 

Test your code. You should see merlons and embrasures nicely spread across the top of the wall.

{{<figure src="/castle/4.png">}}

### Step 5

The next function will set the TNT right next to the gate, place a distinctive trigger at a safe distance and display a message to the player. The setBlock() function takes an additional parameter for the TNT block. Value 1 means that it will be set to a "Ready to explode" state.  See https://pimylifeup.com/minecraft-pi-edition-api-reference/ for other acceptable values for this parameter.

Please put the function definition above the two last lines of your code (connection to Minecraft and buildCastle(). Then, at the very end of the program, add the execution call of the new function.

{{<figure src="/castle/5.png">}}

### Step 6

Test your code. Can you see the TNT and the coloured trigger block? 

Still, the trigger does not start the detonation. That will be our job in the next step. 

{{<figure src="/castle/6.png">}}

### Step 7

The last part of the program will be responsible for detecting if the player stands on the trigger and detonate the TNT. Within an endless "while" loop, the position of the player is read and compared to the coordinates of the trigger block. If the trigger is directly under the player, we will put fire underneath the TNT block which should cause the detonation within few seconds. The "break" statement at the end is used to break the loop and end the program. Otherwise setting up the fire and sending the message might happen again after the detonation.

{{<figure src="/castle/7.png">}}

### Step 8

Test your program. Can you get inside the castle through the damaged gate?

Hint: If you struggle to find the exact spot for the trigger,  press F3 to have your current coordinates displayed. These should match with values of X, Y and Z you set at the beginning of the program.

{{<figure src="/castle/8.png">}}

### Reference code

You can access the code for this project here: https://github.com/wasilpaw/ohsnapcoders/blob/main/detonate.py.

### Challenges

- Add more TNT to destroy a whole wall
- Add even more TNT to destroy the whole castle
- Make the number of TNT blocks relative to the size of the castle but small enough to destroy it fully
- Make your castle more realistic by adding turrets and moat