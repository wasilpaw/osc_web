---
title:       "Let me tell you a joke"
subtitle:    ""
description: ""
date:        2022-02-22
author:      "Pawel Wasilewski"
image:       ""
tags:        ["Minecraft", "Python", "API"]
categories:  ["Tutorials"]
---

In this project, we will build a smart home in Minecraft greeting you with a random joke whenever you enter it. We will do this by combining code from a couple of the projects from “the Adventures in Minecraft” and playing with the Request library for accessing a public API to fetch jokes.

{{<figure src="/joke/thejoke.png">}}

## The Theory and Preparations

### REST API

"API (application programming interface) is a set of rules and mechanisms by which one application or component interacts with the others." See more here https://mlsdev.com/blog/81-a-beginner-s-tutorial-for-understanding-restful-api 

### The joke API

Let's explore the joke API we will use in the project later. Try to run some of the Curl commands from https://icanhazdadjoke.com/api in your command line (CMD)

### JSON

The most common format of exchanging information via the REST APIs is JSON. We will use it in our code to read the data. See more theory and some examples here https://www.w3schools.com/whatis/whatis_json.asp.

### The Request library in Python

We will need to import the "Request" library to use the functions required for sending an API GET request and accessing the response. You might need to install either using PyCharm or in the command line using PIP.

## Implementation

### Build a house
To build the home we will reuse some code we already had from previous project. Go to https://github.com/wasilpaw/ohsnapcoders/blob/main/Neighbourhood.py and copy first 36 lines into your new python file


{{<figure src="/joke/house_code.png">}}

Update the coordinates x,y and z to locate the house in a good place in your world.
**Test** your code. Is there a new house build?

{{<figure src="/joke/house.png">}}

### Detect the player entering the house

To detect the player being inside the house, let's reuse code from https://github.com/wasilpaw/ohsnapcoders/blob/main/rent.py . 
Underneath the house code add slightly modified code from the above source. We will need to point the X1 and Z1 to the coordinates of the house corner.

{{<figure src="/joke/detect_code.png">}}

**Test** your code. You probably will see a constant stream of greetings once you're inside. The greetings should disappear few seconds after you leave the house.

{{<figure src="/joke/detect_first.png">}}

We need to modify the code so the greeting is displayed only at the moment of entering the house. We will need a new variable and a conditional statement. Update the code to match below.

{{<figure src="/joke/detect_entrance_code.png">}}

The hasEntered variable is an indicator if a user has been in the house a moment ago. Using it, we can trigger the message only while inside for the first time.
Test the code. You should see the greeting only once after entering the house.

### Display the joke read from the API

As mentioned previously, we will need to add the request library to send requests and read responses from the remote API. Add the import statement at the top of the file:

{{<figure src="/joke/import.png">}}

Lines 50-52 below is actually one statement that triggers a GET request towards the joke API. The params and headers are required as otherwise, the API will return a full web page rather than just a random joke. The response includes three elements: the joke but also its unique id in the database and the HTTP status code. For the purpose of this project we just need the joke itself so rather than displaying the whole response we just access part of it using the .json created object.

{{<figure src="/joke/joke_final.png">}}

**Test** your code. Your smart home should greet you with a random joke every time you go inside.

If your program is crashing because some of the jokes cannot be decoded properly. Have a look at https://pythonguides.com/remove-unicode-characters-in-python/. 

Full code for reference: https://github.com/wasilpaw/ohsnapcoders/blob/main/jokehouse.py

### Challenges

Try other API with authentication:
- Harry Potter API https://hp-api.herokuapp.com/ 
- Pokemon API https://pokeapi.co/
- Space API http://open-notify.org/
- Sunrise Sunset API https://sunrise-sunset.org/api