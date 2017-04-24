---
title: Set up your own studies
keywords: create, import, export
tags:
summary:
sidebar: mydoc_sidebar
permalink: Set-up-your-own-studies.html
folder:
toc: true
last_updated: 28 Dec 2016
---

So, now you've installed JATOS and tried out all the examples studies. What now?

### Create a new study ###
There are two ways to create a new study:

1. from scratch by pressing the **New Study** button in the header of each JATOS page. Then edit the study properties and add new components manually.

2. take an existing study (e.g. from [Example Studies](http://www.jatos.org/Example-Studies.html)) as a prototype and modify it bit by bit. We recommend you start with this to get a quick idea of how JATOS works. Just import an existing study (e.g. one from the study examples) and clone it by clicking on More --> Clone in the study bar.

### Write your own studies in JavaScript
The most difficult part - though it's still easy! - is to learn to write your own study component scripts, using HTML, CSS and JavaScripts. Or, instead of reinventing the wheel, you could use a framework like jsPsych that helps you with this (see [jsPsych and JATOS](jsPsych-and-JATOS.html)).

Check out the [Mandatory lines in your components' HTML](Mandatory-lines-in-your-components-HTML.html) page to know what you absolutely must include in your scripts in order to let JATOS see them. Also check out the [jatos.js Reference](jatos.js-Reference.html), that contains a set of very useful functions that you have to use to communicate with jatos (to e.g. submit and receive data).
  
If you are a newbie to HTML/JavaScript programming, there are LOADS of free and excellent tutorials online. Like [this one from the Kahn Academy](https://www.khanacademy.org/computing/computer-programming) or more searchable tutorials like the simple ones from the [w3 schools](http://www.w3schools.com/). In addition, [StackOverflow](http://stackoverflow.com/questions/tagged/html) is the best place to solve the problems that hundreds of others have encountered before.  

### Import / Export of studies
Usually you conveniently develop your study on your local computer where you have a [local installation of JATOS](Installation.html). Then just use the export and import buttons in your installations to transfer the study to your [JATOS server](JATOS-on-a-server.html).

1. In the GUI of your local installation press **Export** in the Study Toolbar. JATOS saves your study asset folder and some data about your study and it's components (mostly the properties) into a ZIP file and lets you download it. Leave the ZIP file as it is.
1. In the GUI of your server installations press **Import** in the header. Select the ZIP you saved in step 1. JATOS will upload and unpack your study.

If you have trouble with the export and you are using a Safari browser have a look into [this issue in our Troubleshooting section](Troubleshooting.html#downloading-a-study--exporting-a-study-fails-eg-in-safari-browsers).

### Decide how you're going to recruit your workers and generate the links
Once you have your study running and have it on a server instance, you'll need to get your workers to access your study. [Different types of workers](Worker-Types.html) might be allowed to run your study. You could, but you don't have to, recruit your workers [using MTurk](Connect-to-Mechanical-Turk.html). You could also generate direct links in the [Worker Setup](Run-your-Study-with-Batch-Manager-and-Worker-Setup.html) to send to different workers. 

### Export your result data
After you let workers run your study and you gathered result data you probably want to export them to your local computer for further analysis. Go to one of the **Results** views and select the results you want to export (select them by just clicking somewhere in the row). Then click 'Export Selected'. This will download all your results in one text file. 

### Analyse your data
Once you have collected all your data, export it to text files. If you used the JSON format (which is handy - but any other text is fine too) you can analyse your data using this nice [JSON parser for Matlab and Octave](http://iso2mesh.sourceforge.net/cgi-bin/index.cgi?jsonlab) or the [JSON parser for R](http://cran.r-project.org/web/packages/jsonlite/index.html).
