---
title:       "A website using Hugo"
subtitle:    ""
description: ""
date:        2022-06-09
author:      "Pawel Wasilewski"
image:       ""
tags:        ["Hugo", "web"]
categories:  ["Tutorials"]
---

This tutorial will describe how to build a static website using Hugo.
The main programming language utilised in Websites is the HTML. To see an example of HTML code, right click on this page and choose "View page source". It is pretty complicated, especially if you want to build professionally looking pages.
Hugo allows us to build beautiful websites without the need of knowing HTML.
{{<figure src="/website/hugo diagram.drawio.png">}}


To start with, choose an imaginary company you would build the website for. It might be a football school, cake shop or any other business.


### Install Hugo 

Follow Hugo installation steps for Windows in here 
{{< youtube G7umPCU-8xc >}}
Instructions for other operating systems are here https://gohugo.io/getting-started/installing.

### Install the editor
A good code  editor will make the web development much quicker. While developing Hugo websites, we will be using Markdown files for defining content of the pages and TOML for configuration. 
A good choice for both of these languages might be [Microsoft Visual Studio Code](https://code.visualstudio.com/). It has out of the box Markdown support. You can easily add "Better TOML" extension in the tool. 

### A basic website

Next step is to create a blank website and configure it. 
Within the command line move to the "Sites" folders and type the below command 
{{< highlight Bash>}}
cd c:\Hugo\Sites\
hugo new site example.com
{{< /highlight >}}
You should now have a new folder created called "example.com" with more folders and files underneath.
{{<figure src="/website/basic_website_created.JPG">}}

Each Hugo website needs to use a theme which would be the main UI framework. 
Hugo community offers extensive number of free themes. For this project we will start with "Ananke" theme [demo site](https://gohugo-ananke-theme-demo.netlify.app/).
Download the Ananke theme as a zip from github https://github.com/theNewDynamic/gohugo-theme-ananke/archive/refs/heads/master.zip. Once downloaded, copy the extracted content into "themes" folder of your website and rename the folder to "ananke".
Your folder structure should look like this:{{<figure src="/website/ananke_installed.JPG">}}

We've copied the theme files and the next step is configure the website to use it. Locate the "config.toml" file in "example.com" folder and open it for editing.
Update the title value to a name of your imaginary business and add a new line to define the theme as below
{{<figure src="/website/config_with_ananke.JPG">}}

The website is now ready to be built. In your command line navigate to your website folder and execute "Hugo serve" command.
{{< highlight Bash>}}
cd c:\Hugo\Sites\example.com\
hugo serve -D
{{< /highlight >}}

Your website should be available under [http://localhost:1313/](http://localhost:1313/) and look like {{<figure src="/website/cakesh0p.JPG">}}

### Explore what the Ananke theme offers
At this point your website would look very basic. Let's copy some of the content from the "exampleSite" folder inside Ananke theme location. Please copy all the files from "content" and "static" folders from the exampleSite to the corresponding folders in your main website. Rebuild your website. You should see more content including two categories on the top right.

### New category
Let's add another category. This can be done by creating a new .md file inside the "content/en" folder. Execute the below command in your commnad line terminal.
{{< highlight Bash>}}
hugo new en/offer.md
{{< /highlight >}}
Once the new file is created, copy all of the front matter parameters from contact.md file with the exception of title.
