---
title: Troubleshooting
keywords: troubleshooting, logging, log
tags:
summary:
sidebar: mydoc_sidebar
permalink: Troubleshooting.html
folder:
toc: true
last_updated: 28 Dec 2016
---

### JATOS failed to update the GUI automatically?

Try reloading the browser. 

### Downloading a study / exporting a study fails (e.g. in Safari browsers)

As a default, Safari (and some other browsers) automatically unzips every archive file after downloading it. When you export a study, JATOS zips your study together (study properties, all components, and all files like HTML, JavaScripts, images) and delivers it to your browser, who should save it in your local computer. Safari's default unzipping interferes with this. Follow [these instructions](https://discussions.apple.com/thread/1958374?start=0&tstart=0) to prevent Safari's automatic unzip.

### JATOS fails to start?

<b>(Or, if you are running Windows, do you get the message 'JATOS is already running. Press any key to continue'...)</b>

This will happen if your computer crashed before you had the chance to close JATOS. 

This is what you might see on a Mac Terminal if JATOS doesn't start:

![jatos doesn't start](images/shell_start1.png)

Close any open command prompt windows. Then look into your JATOS folder, and check if there's a file called 'RUNNING_PID'. Delete this file and try to start JATOS again. 

Here is how it should look if JATOS started successfully:

![jatos doesn't start](images/shell_start2.png)
 
### Read log file in the browser

In a perfect world, JATOS always works smoothly and, when it doesn't, it describes the problem in an error message. Unfortunately we aren't in a perfect world: every now and then something will go wrong and you might not get any clear error messages, or no message at all. In these (rare) cases, you can look into JATOS' log file to try to find what the problem might be.  

The standard way to read the log file is directly on the server. You'll find your complete log file in `jatos_directory/logs/application.log`. Because JATOS is designed to avoid the command line interface, we offer a way to view your log file directly in your browser.

Just open the URL `http://your-jatos-server/jatos/log`. For privacy and security reasons, you must be logged in as an **admin** user. For example, if you're running JATOS locally with the standard settings:

[http://localhost:9000/jatos/log](http://localhost:9000/jatos/log)

By default, JATOS will display the last 1000 lines of the application.log file. If you want to see more than the last 1000 lines, add the query parameter `limit`. E.g. to display the last 10000 lines on a local JATOS instance:

[http://localhost:9000/jatos/log?limit=100000](http://localhost:9000/jatos/log?limit=10000)

### A file (library, image, ...) included in the HTML fails to load?

There is a common mistake Windows users make that might prevent files in the HTML from loading: Any URL or file path in a HTML file should only use '/' as a file path separator - even on Windows systems. So it should always be e.g. `<script src="/study_assets/mystudy/jsPsych-5.0.3/jspsych.js"></script>` and not `<script src="\study_assets\mystudy\jsPsych-5.0.3\jspsych.js"></script>`. 


### Database is corrupted?

If you get an error that reads something like: "Error in custom provider, Configuration error: Configuration error[Cannot connect to database [default]]", your database might be corrupted. 

There are two reasons why this might be the case: you moved your JATOS file package while it was running or you installed JATOS in a synched folder. To prevent this, be sure to always be careful with the following:
1. Always stop JATOS (type `/loader.sh stop` in your Unix terminal or close the window on Windows) before moving it.  
1. As we mentioned in the [Installation page](Installation.html), you can run JATOS from pretty much anywhere **except** from a folder that synchs across devices, like Dropbox or Google Drive. Doing so might lead to database corruption, because while the files might be synched between computers, the running processes aren't. This will lead to havoc and destruction and, in extreme cases, to the implosion of the known Universe. You can find in our [blog post](http://blog.jatos.org/Database_Recovery/) a description of an attempt to recover a corrupted database. Didn't work.

**Of course, this brings us to an important point: back up your result data (i.e., simply download and save your text files) regularly if you're running a study!**
