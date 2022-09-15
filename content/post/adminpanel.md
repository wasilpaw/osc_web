---
title:       "Minecraft Admin panel (GUI)"
subtitle:    ""
description: ""
date:        2022-01-02
author:      "Pawel Wasilewski"
image:       ""
tags:        ["Minecraft", "Python", "GUI"]
categories:  ["Tutorials"]
---

In this tutorial, you will learn how to build a GUI - Graphical User Interface. Our goal is to create an admin panel for Minecraft that would execute some of the functions we played with in other projects. In particular, this would be:
- Teleport the player to given coordinates​
- Clear a space based on coordinates of two vertices
- Build a complicated maze based on chosen file and given coordinates

{{<figure src="/gui/Final.png">}}


### Installation

You would need the "PySimpleGUI" package installed. Use PyCharm installer or refer to PIP command on https://ohsnapcoders.com/post/alarmclock/ line if you are using a different code editor.

The default version of "PySimpleGUI" is basically a wrapper on a very popular GUI package tkinter. 
It provides functions to build and organise GUI windows. See https://pysimplegui.readthedocs.io/en/latest/ for an extensive documentation with example of usage.

### Display a window

Start with downloading the basic code from https://github.com/wasilpaw/ohsnapcoders/blob/main/AdminPanel_base.py

{{<figure src="/gui/base_code.png">}}

The program starts with the required imports including the PySimpleGUI.

It also has a modified version of the *buildMaze()* function. This function builds a maze basing on a given CSV file and coordinates. If you need to learn more about the algorithm, please read the related chapter in the "Adventures in Minecraft" book. We will use this function later in the project.

Line 27 is where the layout is defined. The layout is required by PySimpleGUI to determine what buttons and fields should be created and in what order. For now, this is an empty table but soon we will start adding more there.

Line 28 is where the window is created. Margins will define how big should the window be.

The *while* loop is used to continuously check user interaction with the page. For now, it only checks if clicked on the "X".

Try running the code. Can you close the window?

{{<figure src="/gui/base_window.png">}}

### Teleport the player to a new location

Our first action for the admin panel will be to teleport the player to the given coordinates.
We will need three text fields to provide the coordinates plus two buttons: One to execute the teleportation and second to cancel the action.
Definition of the fields is done inside the layout table. Please add the code below.

{{<figure src="/gui/Teleport_layout.png">}}

The values within [] represent a single line in the window. If there's more than one element in a line, they are distinguished by commas.
The *Text()* method display text while *InputText()* creates a field where user can provide information.The values from these fields will be accessible for us while the program is being executed.
The last line includes two buttons, each with a different name / identificator.
Note that the margins in line 33 have been removed from the *Window()* function. Now that we have some elements of the layout, the size of the window will automatically scale.

**Run your program**. You should see something like below:

{{<figure src="/gui/teleport_window.png">}}

At this point, you would not see any difference after clicking on the buttons. That's because we need to handle the events related to user action of clicking on them. 

In the main loop, we need to check if the latest event's name is the same as the name of the button. If the event is related the "Teleport" button, we would execute *setTilePos()* function to move the player into a new position. This function requires us to provide three parameters - the coordinates of the new position. We would use the *values[]* table to access the information put in the window. 

Notice that in line 36 below function *window.read()* assinges all the values from the window fields into the *values[]* table.

Reaction to "Cancel" button clicking should be same as "X" so this event value is added to the line 37.

{{<figure src="/gui/teleport_events.png">}}

**Test your program**. Can teleport your player? Can you close the window by clicking on "Cancel"?

### Clear a space

To clear any space in Minecraft, we will need 6 more text fields to allow the input of the coordinates for two vertices of the rectangular cuboid we are going to change into AIR. We will also need an addition button to execute the clearing. Let's start with modifying the layout to accommodate these extra elements.

{{<figure src="/gui/build_code.png">}}

Test your program. The window should look like:

{{<figure src="/gui/Clear_window_scr.png">}}

The new button is there but nothing happens after clicking on it. That's because it's not yet handled in the code.
To do this, we will add a new conditional statement capturing the event of the user clicking on the "Clear" button (line 52 below).
Whenever this happens we execute the setBlocks() functions with arguments copied over from six new text input fields. Notice that their indices are starting with 3 and ending 8.

{{<figure src="/gui/Clear_event.png">}}

Time to **test the second function**. Note down the coordinates of space you would like to clear in Minecraft and try to empty it using your Admin Panel program.

### Build a maze from file

The third feature of the Admin Panel will allow users to build a maze (or any two-level structure) based on a design in a CSV file.
The layout will have to be modified to allow for a special button to browse files and three more text input fields for the coordinates of the starting point of the maze. Please add lines 40 to 46.

{{<figure src="/gui/build_code.png">}}

**Test your code**. While the build event is not yet handled, you should be able to select a file from your local storage

{{<figure src="/gui/FileSelection.png">}}

To handle the "Build" button, you will need to add one more conditional statement in the main game loop (line 61 below).
In case of the event happening, Python will execute the buildMaze() function with the arguments being firstly the csv file location, then the three coordinates.

{{<figure src="/gui/build_event.png">}}

**Test your program**. If you don't happen to have a csv file with maze design, you can download one from https://raw.githubusercontent.com/wasilpaw/ohsnapcoders/main/maze1.csv .

### Customise how your GUI looks

PySimpleUI provides many ways to customise how the window looks. Try setting up a theme above the layout definition.

{{<figure src="/gui/theme.png">}}

**Test your program**. Did the colours of the window change?

{{<figure src="/gui/themedUI.png">}}

Search online for different themes supported by PySimpleUI. 
Check also the documentation for *Text()*, *InputText()* and *Button()*. What else can you change visually?
Hint: in PyCharm, click on one of this functions and press "CTRL+Q". You should get documentation with optional parameters described, for example background or text colour.

### Secure the program with a login window

Our program might be quite dangerous in wrong hands. You would not like your brother/sister to run it and wipe out half of your world. We could protect the admin panel by introducing a password. To do this, we will create a window asking for a password and compare it with the predefined one. The first step to do is to add the definition of a new window. The code below should be inserted right below the buildMaze() function definition.

{{<figure src="/gui/Login_screen.png">}}

This definition is very similar to what we used in the main window with two exceptions. Firstly, there's the "password_char" parameter for the function InputText(). By defining a character here, we will mask the characters typed in by the user. This is a standard security practice protecting the password from adversaries watching over the shoulder or watching screen recordings. "*" is the standard password masking character but why not use a different one? Feel free to experiment here. 

The second new element is the "key" parameter of the Text() function defining the last field on the bottom. By using keys, we can update UI field content from the code level. In our case, this field is initially empty but we will use it to display a message in case the user types a wrong password.

**Test** your program. Right after running it, you should see a new window as below.

{{<figure src="/gui/Login_screen_view.png">}}

Time to add code to handle events. Right below the definition of the new login window type the following (or copy the previous event loop and just update to match):

{{<figure src="/gui/Login_screen_handler.png">}}

The first thing you can notice is the exit(0) function call in an event of the user closing the window. The function exit() closes the program execution immediately. Parameter 0 indicated that everything was fine. Other values could be used to signal abnormal closure like insufficient computer resources or another unexpected error.

The main logic related to security starts in line 38 above. The conditional statement compares the content of the input text field to the predefined password. In case of a match, the login window is being closed and the loop breaks which moves the execution to the main part of the program.

The last line covers a case where the password did not match. Here, the "Status" field is field is update with the relevant message and the user would have another chance to enter the password.

Test your program. Does it pass through the login screen when the password is correct? Can you see the "Wrong Password" message when there is no password match?

{{<figure src="/gui/Login_screen_wrong.png">}}

### Reference code

You can access the code for this project here: https://github.com/wasilpaw/ohsnapcoders/blob/main/adminpanel.py

### Challenges

- Try to help your users select the right kind of file. Currently, your program accepts all files. Can you display a message when the selected file extension is not ".csv"?
- The login window allows infinite attempts to try passwords. This is a potential vulnerability as a brute force attack could be applied to crack the password. Can you limit the number of failed attempts and close the program after this limit is reached?
- PySimpleUI supports pop-up windows. Can you display a pop-up window for the "Wrong Password" message?