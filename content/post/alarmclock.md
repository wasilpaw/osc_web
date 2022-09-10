---
title:       "Minecraft alarm clock"
subtitle:    ""
description: ""
date:        2021-02-04
author:      "Pawel Wasilewski"
image:       ""
tags:        ["Minecraft", "Python"]
categories:  ["Tutorials"]
---

In this tutorial, you will learn how to read system time and play sounds. We will use "playsound" and "datetime" libraries as part of the program that will display the current time in Minecraft using a slightly unusual way, by building stacks of blocks. The height of each stack will represent the current value for hours, minutes and seconds. A the beginning, the user will be asked to provide the time when the alarm should be fired and a respective sound played.
{{<figure src="/alarmclock/MineClock.gif">}}

### Installation
The "playsound" library will be required to guess what: play a sound! It could be installed on your computer using Python's package manager PIP or directly from PyCharm Edu (the easier option).

If you decided to go for manual PIP install, firstly open the command line (Windows key and type cmd). Then change the directory to the location of your Python installation and execute two pip commands as below.

{{< highlight Bash>}}
cd AppData\Local\Programs\Python\Python36
python -m pip install --upgrade pip
python -m pip install --upgrade playsound
{{< /highlight >}}

### Imports and definitions of the variables
Start with importing 5 libraries. "Datatime" will be used to read the system time while "time" includes the sleep() functions that we will use to introduce time gaps between reading the system time and updating the clock display.

We will also need 3 constants to define the position of the clock (please update these to the coordinates where you would like to place the clock!) and 5 more variables. AHour and AMinute will store the values given by the user. CHour, CMinute and Csecond will be update every second and used to determine how high should the block stacks be.
{{<figure src="/alarmclock/Variables.png">}}

### Functions and the main loop
The main logic of the alarm clock starts with setting up the alarm. Then, in the main loop we would read the current time, display it in Minecraft and wait 1 second before the next update.  The alarm would be fired only if the hours and minutes for both current and alarm time are the same. Once the alarm is fired, the "break" statement would break the loop and end the program.

All the functions definitions would initially be empty but we will fill them in later.

Please write this code after the definitions of the variables. 
{{<figure src="/alarmclock/FunctionsLoop.png">}}

Try running the program. If no errors occur, the program should finish straight away as both the alarm and the current time variables are set to the same values at this stage.

### Reading the current time
The current system time can be read using "datetime" library. The datetime.now() function returns an object that holds multiple parameters representing the current calendar date and time of the day. We will use only the three time-related attributes of this object and assigned them to the relevant variables.

Remember to use the "global" keyword. It tells Python interpreter to store the values in the global context of the variable. Otherwise, the values would not be available outside of the function body. 

Please replace the "pass" keyword under the definition oft the "readCurrentTime()" function with the below code.

{{<figure src="/alarmclock/ReadTime.png">}}

**Test** your program. There should be two changes. Firstly the program should not finish immediately. This is because the condition inside the loop is not met now because the current hour and minute are being updated. Secondly, you should have the latest system time printed out in the Python console once every second.

### Display the current time

Displaying the clock will be simplified and each value of the current time will be represented by one stack of blocks.

We start with clearing the area for the three stacks. This needs to be done every time the current time is being displayed because after reaching the maximum value for a variable (for example 59 seconds) the next value would have to be fall to a minimum.

Then there's one column for each variable containing the latest time element.

{{<figure src="/alarmclock/DisplayFunct.png">}}

**Test** your program. You should see some stacks being built and they should change every second. Do they reflect the current time?

{{<figure src="/alarmclock/Display_M.png">}}

### Set the alarm

Time to set the alarm. We will use the built-in "input()" function that displays the message and return the string typed in by the user. We will then need to cast this string to integer by using "int()" function. This is required so that the values could be later compared to the current system time.

{{<figure src="/alarmclock/SetAlarmFunct.png">}}

Test your program by setting up the alarm time to be a minute in the future. Does you program stop after reaching the set alarm time?

### Fire the alarm

Let's add a sound to make sure our alarm will not be missed out.
You will need an .mp3 or .wave file saved in the folder where your program is located. If you don't have it yet, try downloading something from https://orangefreesounds.com/sound-effects/. 
The "playsound()" function needs only to take the name of your file so make sure you write your own rather then the one below.

{{<figure src="/alarmclock/FireFunction.png">}}

**Test** your program. Can you hear the sound when the alarm time is reached?

### Challenges

- Add code that would do something visually striking with the clock once the alarm is fired
- Add seconds to the alarm setup
- Validate the input so that the programs does not start if the values are wrong