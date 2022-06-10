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


### Installation and initial configuration

Follow the Hugo installation steps in here https://gohugo.io/getting-started/installing#windows.

Next step is to create a blank website and configure it. Apply steps 2 to 6 from https://gohugo.io/getting-started/quick-start/#step-2-create-a-new-site.
Step 3 requires git installed to use the theme. We will be using git later but for now, you can simply download the Ananke them as a zip from github https://github.com/theNewDynamic/gohugo-theme-ananke/archive/refs/heads/master.zip. Once downloaded, copy the folder into "themes" folder of your website and rename it to "ananke".

### Install the editor
A good code  editor will make the web development much quicker. Try [Microsoft Visual Studio Code](https://code.visualstudio.com/). It has out of the box Markdown support. You can easily add "Better TOML" extension in the tool. TOML is the language used for the site configuration.

### Explore what the Ananke theme offers
At this point your website would look very basic. Let's copy some of the content from the "exampleSite" folder inside Ananke theme location. Please copy all the files from "content" and "static" folders from the exampleSite to the corresponding folders in your main website. Rebuild your website. You should see more content including two categories on the top right.

### New category
Let's add another category. This can be done by creating a new .md file inside the "content/en" folder. Execute the below command in your commnad line terminal.
{{< highlight>}}
hugo new en/offer.md
{{< /highlight >}}
Once the new file is created, copy all of the front matter parameters from contact.md file with the exception of title.
