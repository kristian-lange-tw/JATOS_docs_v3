---
title: Moving from a Local to a Server Installation
keywords: local installation, server installation
tags:
summary:
sidebar: mydoc_sidebar
permalink: Moving-from-a-Local-to-a-Server-Installation.html
folder:
toc: true
last_updated: 13 Aug 2019
---

## Preparing your study

We recommend that you always start to work on a new study in a *local* installation of JATOS. That means, [download and run JATOS on your local computer](Installation.html#easy-installation-on-your-local-computer). 
The main advantage of this is that you have easy access to all your HTML files and assets and can move them around, delete, and replace without any fuss. 

## Opening your study to the WWW

Once your study scripts are complete and bug-free, you need to make them available through the Internet. For that you will need, of course, [a server](JATOS-on-a-server.html).

If you have a server, you will need to take your ready-to-run study from your local installation and deploy it to a server. In order to do this:
1. On your *local* JATOS installation, where your study is, click on the study you want to export on the left sidebar. 
1. On the Study bar, click Export. A pop-up window will appear. Save the .jzip file wherever you like on your computer.  
1. On your *server* installation, simply click Import. 

Done. 

Here's a little sketch of the same three steps above
![jzip workflow](images/jzipWorkflow.png)


Please not that:
* The two JATOS look almost identical, and you will (basically) only distinguish them on the basis of the URL in the browser. To prevent confusion, we've made it easier: A local JATOS installation has a black bar on top. A server installation has a light-grey bar. 
* A .jzip file is a normal .zip file. We just changed the name to make this process clearer. (JATOS users got confused and always tried to unzip the file they had downloaded, add HTML files in it, and re-zip it. This will lead to all sorts of problems. Don't do this. 
You should do all modifications of files and study properties from the JATOS GUI.)

