---
title:       "Minecraft Escape Room"
subtitle:    ""
description: ""
date:        2021-02-15
author:      "Pawel Wasilewski"
image:       ""
tags:        ["Minecraft", "Python"]
categories:  ["Tutorials"]
---

The objective of this tutorial is to build an escape room in Minecraft. The player would be challenged to answer questions to leave the room. In the unlucky event of a wrong answer, the floor will disappear causing the player to fall into a lava pit.


### Step 1

Start with creating a new python file named escaperoom.py. 

At the beginning of the program, we will define a few constants that will be used later. Values of X, Y, Z should be ideally adapted to your Minecraft world so that this starting point is right over the ground and the player can leave the room after successfully answering all the questions. 

The last three assignments are the colours of the WOOL blocks we will use for answering the questions.

Finally, we establish the connection to the Minecraft server.

{{<figure src="/escape/1.png">}}

### Step 2

The first function will encapsulate all the building involved in the creation of the escape room. It will also teleport the player inside the room.

{{<figure src="/escape/2.png">}}

### Step 3

Now let’s test the code. Before running the program do ensure your Minecraft game is in Survival mode. This will make the game more realistic as you should not be able to break out of the room by simply destroying the walls. Make sure you have an iron sword in your inventory - it will be needed for interactions during the game. 

To change the mode to survival, switch to the server window and type the following command:

{{< highlight Bash>}}
Gamemode survival <playername>
{{< /highlight >}}

Now run the program.

You should end up in a torch-lit room with 3 coloured blocks in the middle. 

Can you get out of the room?

{{<figure src="/escape/3.png">}}

### Step 4 

Now right underneath the definition of the first function and above the buildEscapeRoom() function call, please add two more functions that will modify the room. We will use them later in the main logic of the game.

{{<figure src="/escape/4.png">}}

### Step 5

To test these two new functions we will temporarily add 4 more lines of code at the end of the program (38-41 on the screenshot below). You should delete them after this part of the testing is completed. We don’t need them for the game but it’s important to test the code incrementally and in small chunks.

{{<figure src="/escape/5a.png">}}

You should see an entrance appearing in one of the walls after 4 seconds. After another 4 seconds, the floor should disappear and you should fall into the lava pit.

{{<figure src="/escape/5b.png">}}

Remember to delete the last 4 lines of code (38-41 on the screenshot above).

### Step 6

The last function will cover the check of the player’s answer which will be given by hitting (right-click with an iron sword selected) one of the three coloured blocks in the middle of the room. As we don’t know when the player will answer, the function checks all the hit events every second and compares the colour of the hit block with the value passed as an argument to the function. Logical True is returned if the colours match indicating a correct answer.

Please add this code above the *buildEscapeRoom()* function call.

{{<figure src="/escape/6.png">}}

### Step 7

Now, let's go to the main logic of the game which will use all of the previously defined functions. After displaying some initial text, the user will be given a question with three answers. Then the selected answer will be validated with checkAnswer() function. The doors will open only if all the questions are answered correctly.

The first line below should already be present in your program. Add the remaining lines at the bottom of your program.

{{<figure src="/escape/7.png">}}

### Step 8

Test it. Are you falling into the lava pit after a wrong answer? Can you escape the room when all questions are answered correctly?

{{<figure src="/escape/8a.png">}}
{{<figure src="/escape/8b.png">}}

### Reference code

You can access the code for this project here: https://github.com/wasilpaw/ohsnapcoders/blob/main/escaperoom.py

### Challenges

- Replace the questions and answers with your ones. Remember to adapt the parameter of the check function if needed. 
- Add the third question.
- Add a limit of time for answering a question.