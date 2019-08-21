---
title: JATOS Workflow
keywords: local installation, server installation
tags:
summary:
sidebar: mydoc_sidebar
permalink: JATOS-Workflow.html
folder:
toc: true
last_updated: 21 Aug 2019
---

## Workflow: What JATOS does

When you start working with studies online, it can be hard to see what exactly JATOS does. This page, explaining the general workflow, might help to clarify things. 
![general workflow](images/generalWorkflow.png)

## Step 1: Create/edit HTML, JS, and CSS files (Prepare your study) 

We recommend that you always start to work on a new study in a *local* installation of JATOS. That means, [download and run JATOS on your local computer](Installation.html#easy-installation-on-your-local-computer). 
The main advantage of this is that you have easy access to all your HTML files and assets and can move them around, delete, and replace without any fuss. 

## Step 2: Deploy files to a server (Make your study available to the WWW)

Once your study scripts are complete and bug-free, you need to make them available through the Internet. For that you will need, of course, [a server](JATOS-on-a-server.html).

If you have a server already, you will need to take your ready-to-run study from your local installation and deploy it to the server. In order to do this:
1. On your *local* JATOS installation, where your study is, click on the study you want to export on the left sidebar. 
1. On the Study bar, click Export. A pop-up window will appear. Save the .jzip file wherever you like on your computer.  
1. On your *server* installation, simply click Import. 

Done. 

Please note that:

* The two JATOS look almost identical, and you will (basically) only distinguish them on the basis of the URL in the browser. To prevent confusion, we've made it easier: A local JATOS installation has a black bar on top. A server installation has a light-grey bar. 
* A .jzip file is a normal .zip file. We just changed the name to make this process clearer. (JATOS users got confused and often tried to unzip the file they had downloaded, add HTML files in it, and re-zip it. This will lead to all sorts of problems. Don't do this. 
You should do all modifications of files and study properties from the JATOS GUI.)
* In the process of exporting/importing you'll be moving all HTML/JS/CSS files, along with any assets (images, audio, etc) contained in the local study folder. You will also move the study and component properties (whether it's a group study, allowed worker types, HTML files associated with each component, and much more). You will **not** move result data. 
* If you want to make changes to a study, we also recommend that you do that locally, then again Export locally->Import into the server. If you do this, there will be one more step where you have to confirm that and whether you want to replace the study assets properties.

Here's a little sketch of the same three steps above
![jzip workflow](images/jzipWorkflow.png)


## Step 3: Collect data
You can do this in many different ways, decide which kind of [worker permissions](Worker-Types.html) you need. 

## Step 4: Download and analyze data
One of JATOS' git advantages is that you can manage the results stored in the database without having to type sql commands in a terminal. Instead, just do this [using the GUI](Manage-Results.html)
You'll download a .csv or JSON-formatted text file (depending on how you wrote your JavaScript). We always recommen JSON format because it's more flexible and robust, and use [JSONlab](https://de.mathworks.com/matlabcentral/fileexchange/33381-jsonlab-a-toolbox-to-encode-decode-json-files) to read the data into Matlab and the [rjson](https://cran.r-project.org/web/packages/rjson/index.html) package for R.

