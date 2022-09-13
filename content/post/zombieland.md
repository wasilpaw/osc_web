---
title: "Zombieland"
date: 2022-03-05T22:01:15Z
draft: false
author: Pawel Wasilewski
tags:        ["Python", "Minecraft","OOP"]
categories:  ["Tutorials"]
---

In this project, we will build a game involving zombies.
{{<figure src="/zb_arena.JPG">}}
Each zombie will be represented by two blocks on a square arena. They will be able to move around the arena. Each zombie will be controlled using an instance (object) of a class. Player will need to walk between zombies and avoid bites.

### Classes and objects
Classes and objects are related to Object Oriented Programming and provide a good way to neatly structure code around common behaviours. You can learn about them from these two videos:
* [Introduction to Classes and Objects](https://www.youtube.com/watch?v=8yjkWGRlUmY)
* [Classes and Objects with Python](https://www.youtube.com/watch?v=wfcWRAxRVBA)

## Implementation
### Base code
You start with the base code that will build the arena and create two zombies. Each zombie will be based on the Zombie class.
A zombie will have it's coordinates and colour. The class definition includes the constructor __init__() which builds the zombie based on the coordinates passed as arguments

Copy the below code into a new python file.
{{< highlight python >}}
import mcpi.minecraft as minecraft
import mcpi.block as block

mc = minecraft.Minecraft.create()

### begining of Zombie class definition
class Zombie:

    # the constructor
    def __init__(self, x, y, z):
        self.x = x
        self.y = y
        self.z = z
        self.colour = 13  # zombie will be green
        mc.setBlock(self.x, self.y, self.z, block.WOOL.id, self.colour)  # build the bottom block of the zombie
        mc.setBlock(self.x, self.y + 1, self.z, block.WOOL.id, self.colour)  # build the upper block of the zombie

### end of Zombie class definition

X1 = -50  # coordinates of the first corner
Y = 74
Z1 = -390
SIZE = 20
X2 = X1 + SIZE  # coordinates of the opposite corner depends on the SIZE constant
Z2 = Z1 + SIZE

mc.setBlocks(X1, Y, Z1, X2, Y + 3, Z2, block.AIR.id)  # clean up the area
mc.setBlocks(X1, Y - 1, Z1, X2, Y - 1, Z2, block.BEDROCK.id)  # build the ground
mc.player.setTilePos(X1, Y + 10, Z1)  # teleport the player above the zombieland

first = Zombie(-47, 74, -388)  # create the first Zombie object within the arena
{{< /highlight >}}
Test your code. You should see a Zombie (two green blocks) on the arena.
### More zombies
We need more zombies. Add two or three additional zombies, each in a different location within the arena. To do this, copy the line where the first instance of zombie has been created. Ensure each zombie has been assigned to a new variable.
Test your code. Can you see all of the zombies?
Let's add randomness when defining the location of the zombies by using randint() as X and Z parameters of the constructor. The range for the randint() should match the area limits.

{{<figure src="/zb_random_location.JPG">}}
Apply the randomness to all your zombies.
Test your code

### Getting the zombies to move
Our zombies are bit static. We will add a simple method to make the zombies move.
Add the below code within the Zombie class definition. The indentation should match the constructor.
{{<figure src="/zb_move.JPG">}}
In addition, we should call this new method for each zombie. Let's do it within a loop at the very end of the code. Adding the sleep() function will slow down our zombies. Remember to include time library at the top of your program.

{{<figure src="/zb_loop.JPG">}}

Test your code. Are all the zombies moving?

### Zombies move randomly
Randomness plays an important role in games as it makes events less predictable and more unique.
We can make the zombies move in different directions. We will use random.randint() function. By defining the range for both x an z to be between -1 and 1 we will cover all 8 blocks on the arena surrounding a zombie. One of the options is also that the zombie will not move. This will happen when both randint() calls return 0.
Please add a new method within the Zombie class definition.
{{<figure src="/zb_random_move.JPG">}}

Let's also call these new methods within the loop instead of the .move() method for each of your zombies.
{{<figure src="/zb_move_random_loop.JPG">}}
Test your code. Are the movements random?

### Zombies spawn in random location
We can also start with creating the zombies on the random locations within the arena.
To do this, we will get the random coordinates where the range will be taken from the arena ranges.
Modify the code section where the zombies are created.
{{<figure src="/zb_random_spawn.JPG">}}
Test your code.

### Runaway Zombies
While testing you might have noticed that our zombies don't respect the boundaries of the arena...
{{<figure src="/zb_runaway_zombie.JPG">}}
We need to explicitly limit their moves if the new coordinates would lie outside of the arena.
Add the below conditional statements and the new variables inside the randomMove() method.
{{<figure src="/zb_limits.JPG">}}

Test your code. You might try to temporarily hardcode the coordinates of your zombie and place it on the edge of the arena so that it's quicker to validate the changes. Zombies on the edge should be static more often (4/9 chances to stand still vs 5/9 to move).

### The player in the arena
Lets firstly teleport the player to the corner of the arena.
Please update the "setTilePos()" so that that y coordinate matches the arena.

{{<figure src="/zb_teleport.JPG">}}

The player should not be able to avoid zombies by flying over them. We will ensure this by checking the y coordinate and bringing player back to the arena level if needed.
Create a new function "checkPlayerlocation()" just below the Zombie class definition.

{{<figure src="/zb_location_check.JPG">}}

Now add the function call within the main game loop.

{{<figure src="/zb_location_call.JPG">}}

Test your code. Is the player starting from the corner of the arena. What happens if you try to fly or dig under?

### Zombies chasing the Player
Zombies are not very smart but when they smell the player they will chase her.
Let's add two more methods that will make the zombie capable of walking towards the player.
Please add the below code inside the Zombie class definition. Remember to keep the same indentation as the other methods.

{{<figure src="/zb_chase_code.JPG">}}

Let's look into these two functions in more details starting the with walk() method. You might have noticed that that code in that function looks very similar to randomMove(). In both chasing and randomly moving modes, the zombie has to do the same physical move. Rather then having the same code in both methods, we will extract it into a new method which could be then called from any other function that would require walking. This is an implemantion of a software engineering principle called DRY - Don't Repeat Yourself.
The walk() method includes all the checks that we had before plus one new. At the begging of the function, the move is not allowed if another zombie already occupies the target location.

The main logic in chasePlayer() method is to determine the direction of the next step.
Let's look at an example.
{{<figure src="/zb_example.JPG">}}

The player's coordinates here are (5,25) while our zombie stands at (7,25). To identify the new location for a zombie, we will subtract the X coordinates, 5 - 7 = -2. Every time the result is negative, we will lower to value of X coordinate for the zombie's next move. In case the result would be positive, zombie should go the opposite way. Thus, the x coordinate would be increased.

Let's call the chasePlayer() function for one of the zombies in the main game loop.
{{<figure src="/zb_chase_call.JPG">}}

Test your code. Is one of the zombies chasing you? What happens if you run away from the arena?

### Zombies chasing only if the player is close
Our zombies should chase the player only if it's close enough to smell him.
We already have one method for walking randomly and one for chasing. We can now rewrite the move() method to activate either one or the other. This will depend on the distance between the zombie and the player.
Update the move(self) method so that it has the below code.
{{<figure src="/zb_move_new.JPG">}}
In addition, update the main loop function so that the updated move() method is called.
{{<figure src="/zb_loop_move_new.JPG">}}
Test your code. Are zombies chasing the player when the distance is 5 or less blocks? Can you change the code to make the zombies sense you for a longer distance?

### Zombies bite
Zombies are known to bite people... The player will get three lives and every bite will take one life. The game would finish when the last life is lost.

We will need a new variable for holding the number of remaining lives. Add the line marked with red below. This should be added somewhere below the Zombie class definition but above the main game loop.
{{<figure src="/zb_lives_init.JPG">}}
We will also need a new method to execute the biting. Add the below code within the Zombie class definition. Again, remember that all class methods should have the same indentation.
{{<figure src="/zb_bite.JPG">}}
The bite() method should be called only when Zombie stands exactly next to the player.
Add the following three lines inside the .move() method.
{{<figure src="/zb_move_bite.JPG">}}
Test your code. Do you get a message about being bitten when the zombie stands next to you?

We still need to finish the game if the number of remaining lives is down to zero.
Add this code at the bottom of the main game loop.
{{<figure src="/zb_lives_loop.JPG">}}
Test your code. Does the game finish after three bites? You would still be able to move around but the zombies would be still because your program finished executing.

### Large number of zombies
We could add more zombies by creating more objects one by one. However, this would increase the size of the code and for each of them we would need to create a separate variable. It is far more flexible to use lists and iterate over them with loops.
As the first step, please remove the lines of code where you previously created Zombie objects.
Then add the lines marked as red below. This should be placed at the very bottom of you program where the main game loop is.
{{<figure src="/zb_zombie_list.JPG">}}
The first section (lines 104-108 on the picture) is responsible for creation of a configurable number of zombies. They are being added one by one to the list.
The code in lines 113-114 iterates over each zombie in the list and executes the basic move() method on it.

Test your code. Can you see 5 zombies walking? Try increasing the number. The number of zombies would have an impact on the performance. Remember that performance depends also on your computer's resources.

### Steve collecting diamonds
The player will have an opportunity to increase the number of lives available by collecting diamonds. At any point of time there will be one diamond and its location will be randomly determined.
Let's create a new function for checking if a diamond has been collected by the player. This function definition should be placed above the main game loop but outside of the zombie class.
{{<figure src="/zb_diamond_funct.JPG">}}
The function uses the pattern we applied in some other projects already where all of the hit events are checked. Once we identify a block of diamond type as hit, we would increase the counter of available diamonds. If the new number of diamonds equals the predefined ratio for a new life, we would increase the number of lives and zero the diamonds counter. Once a diamond is collected, it should vanish and a new diamond should be created.
Remember to initiate the values for the DIAMONDS_PER_LIFE constant and diamondsInBackpack variable outside of the function definition (last two lines in the picture above).
Now that we have the function defined, we need to to add code to create the first diamond just before the main game loop and add the function call within the loop. Add the two lines marked with red below to your code.
{{<figure src="/zb_diamond_check.JPG">}}
There is a scenario that we need to handle and that's when a zombie would like to walk onto a diamond block. In that case, we would lose the diamond as it would be overwritten by Zombie block.
To prevent this we need to extend the conditional statement in the walk method to stop zombies if the target location already contains a diamond. Update the line inside walk() method marked as red.
{{<figure src="/zb_walk_check.JPG">}}

Test your code. Can you spot a diamond within the arena? Do you see a message once you right click on the diamonds from short distance (you might need to hold a sword for this to work)? Do you get an extra life once you collected 5 diamonds?

### New zombies appear over time
The game will get more difficult the longer you play it. We will achieve this by gradually adding more zombies to the arena. Add the lines marked with red below.
{{<figure src="/zb_new_zombies.JPG">}}
We start with initiating NEW_ZOMBIE_FREQUENCY constant which defines how many iterations must take place for a new zombie to be created. We will be using "iteration" variable to count how many iterations passed.
The new conditional statement is using the module operator "%". It returns the reminder from division of the two numbers. The "iteration" variable is incremented by 1 with every iteration and only once every 5 iterations the reminder from division will be equal 0. At that moment we will create a new zombie and add it to the list.

Test your code. Do you have new zombies popping up?

### Counting time
The player needs to stay alive for as long as possible. In this step, we will measure the time.
We will need to import the datetime library.
{{<figure src="/zb_date_time.JPG">}}
We will take a timestamp at the beginning of the game and at the end. Subtracting the two will give the number of seconds to display.
Add the lines marked with red to your code.
{{<figure src="/zb_time_check.JPG">}}
Test your code. Does it display the number of seconds for the game?

### Become a beta tester
Beta testers are people who test early versions of applications and are actually paid to do that. Your goal as a beta tester is to find bugs but also provide guidance how playing the game might be more enjoyable.
To do that, you can test different combination of the game parameters. For example, you could tweak the size of the arena ("SIZE"), how many zombies are created at the start ("NUMBER_OF_ZOMBIES"), how often are new zombies created ("NEW_ZOMBIE_FREQUENCY"), how short are the gaps between iterations (the argument of time.sleep()), how many diamonds are required for a new life ("DIAMONDS_PER_LIFE") or how far can zombie sense you ("ZOMBIE_SMELL_RANGE"). Test different values of these parameters.

### Challenge - performance tuning
​While testing with some, more demanding combination of parameters (for example with a large number of zombies) your game will probably not be very responsive. Performance tuning is a form of refactoring where the code is modified with the aim to improve, among others, the responsiveness while keeping the same functionality.

In the case of our game, one of the biggest culprits for performance is the mc.player.getTilePos() function. Every time this function is called, the information needs to be read from the server and that takes time even if both applications are running on the same computer. The main problem is that we are calling this function multiple times (can you count how many?) during a single iteration of the main game loop even though the player's location would probably stay the same for such a short time.
The solution to this problem is to read the player's position once and pass the value to other functions as an argument.

On the main game loop code, it could look like this:
{{<figure src="/zb_tuning.JPG">}}
You would have to modify the relevant functions' definitions to accept the parameter and use it in their body instead of calling the mc.player.getTilePos() function.

Test your code. Can you see an improvement?
