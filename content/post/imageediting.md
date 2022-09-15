---
title:       "Creating a meme: Image editing with Pillow"
subtitle:    ""
description: ""
date:        2021-03-03
author:      "Pawel Wasilewski"
image:       ""
tags:        ["Pillow", "Python"]
categories:  ["Tutorials"]
---

Using Python and the Pillow library you can easily edit images similarly to using a photo editing tool like Photoshop. We will use Pillow to create a meme but firstly we will play with some of the basic functions of the library.

{{<figure src="/meme/Pillow.png">}}


### Installation

Pillow library could be installed on your computer using Python's package manager PIP.

For Windows, firstly open the command line (Windows key and type cmd). Then change the directory to the location of your Python installation and execute two pip commands as below.

{{< highlight Bash>}}
cd AppData\Local\Programs\Python\Python36
python -m pip install --upgrade pip
python -m pip install --upgrade Pillow
{{< /highlight >}}

{{<figure src="/meme/PillowInstall.png">}}

### Changing image format

Let's start with a simple program changing the format of the image. 

Firstly prepare an image file and save it to the same folder where your python program will be located. You could use the below picture or any of your own.

{{<figure src="/meme/pillars.jpg">}}

Now create a new python file using Idle or PyCharm and save it the same location as the picture. Try the below code.

{{<figure src="/meme/formatconversion.png">}}

This program opens the jpg file and saves it as a bitmap. The last two lines results in the picture being displayed.

Check you folder after running the program. Is there a new file? Notice the difference in size.

The *save()* function can automatically detect the format based on the extension in the image name. Try different formats like ".png".

### Reading image metadata

An object of the class "Image" has got many other useful functions and attributes. In the next program, we will look at the latter and display some information about the picture. Try the below code.

{{<figure src="/meme/info_code.png">}}

The outcome will depend on the file you've chosen but might be something similar to the below.

{{<figure src="/meme/info_output.png">}}

### Resizing an image

Our "pillars.jpg" file has a high resolution. We will resize it to a smaller resolution using the code below.

{{<figure src="/meme/resize_code.png">}}

The displayed image should be much smaller then the original one.

### Rotate an image

It might happen that you receive a file that needs rotating. Let try to rotate the below image of flowers.

{{<figure src="/meme/flower.jpg">}}

{{<figure src="/meme/rotate_code.png">}}

You should see the picture now in a horizontal orientation. Try different angles...

### Brightness

Some pictures can benefit from a change of brightness.

{{<figure src="/meme/cat.jpg">}}

{{<figure src="/meme/Bright_code.png">}}

### Contrast

The code is similar to the above with just the name of the enhancer different.

{{<figure src="/meme/contrast_code.png">}}

### Creating a meme

To create a meme we will have to overlap one picture with another and add text on top of it.

Start with downloading the background file and the "Success Kid" pictures. You can as well use your own images here but that would require some changes later in the code to adjust for different image sizes and resolutions.

{{<figure src="/meme/meme_back.png">}}
{{<figure src="/meme/successkid.png">}}

The code below will firstly insert the top picture over the background starting with the pixel passed as the second argument for the function *paste()*. The next step is to define the font type, size and location for each of the two text lines.

{{<figure src="/meme/meme_code.png">}}

The meme should look like this:

{{<figure src="/meme/meme.png">}}

Now change the text and to create your own meme. Modify the size of the text and location so that it's fits visually. You can also try different font types. Check the list of the pre-installed Win10 fonts HERE.

### Reference code

You can access the code for this project here: https://github.com/wasilpaw/ohsnapcoders/blob/main/meme.py

### Challenges

Pillow library has many more functions. You could flip images, crop, create thumbnails, apply filters that could detect contours. Try some of the examples from below:​
- https://pillow.readthedocs.io/en/stable/reference/Image.html#
- https://www.tutorialspoint.com/python_pillow/python_pillow_quick_guide.htm
