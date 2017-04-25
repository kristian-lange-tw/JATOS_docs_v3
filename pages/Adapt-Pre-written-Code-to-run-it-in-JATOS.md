---
title: Adapt Pre written Code to run it in JATOS (Jatosify)
keywords: jatos.js, jatosify, javascript, jsPsych, initialize
tags:
summary:
sidebar: mydoc_sidebar
permalink: Adapt-Pre-written-Code-to-run-it-in-JATOS.html
folder:
toc: true
last_updated: 29 Dec 2016
---

**Make Your Existing Code Run in JATOS - or How To Jatosify a Study** 

You might have a  task, experiment, survey, or study running in a browser. You might have all its files like HTML, JavaScripts, images, etc. Maybe you wrote it with [jsPsych](http://www.jspsych.org) or got it from [The Experiment Factory](http://expfactory.github.io). Do you want to run it with JATOS? That's easy! 

### Create the study in JATOS

1. Create a new study with the '**New Study**' button in JATOS' header. Choose a study title and a folder name. Leave the other fields empty for now and click 'Create'. JATOS will have created a new folder within your assets root folder (default is `/path_to_your_JATOS/study_assets_root/`).
1. Copy all your files (HTML, JavaScripts, images, audio, ...) into your new study folder. 
1. Back in the JATOS GUI, and within the newly created study, create a **new component** by clicking 'Components' and then 'New'. Choose a component title and set the HTML file name, to the name of the HTML file you just copied into the study folder.
1. In your HTML and JavaScripts, change all paths to your **study assets** folder: Always use the prefix `/study_assets/` and then the study assets name you specified in your study's properties when you created it.

    * E.g. if you load the CSS file `snake.css` and the study's assets name is `group_snake` use `<link rel="stylesheet" type="text/css" href="/study_assets/group_snake/snake.css" />`
    * Or if you want to load some JavaScript from your local study assets with the name `prisoner_dilemma`, e.g. the jQuery library, use `<script src="/study_assets/prisoner_dilemma/jquery-1.11.1.min.js"></script>`

✰ Make sure you understand the difference between the `study_assets_root` folder and the placeholder `study_assets` in your path names. `study_assets_root` is the folder in your system (or in the server) where the assets (HTML, JS, CSS, images, etc) of **all** your JATOS studies will be stored. You can [configure](Configure-JATOS-on-a-Server.html#study-assets-root-path) the location of this folder. `study_assets`, on the other hand, is just a placeholder that will go in your HTML files. JATOS will interpret this and replace the placeholder with the path you entered in the field 'Study assets directory name' in your Study's Properties. The advantage of this is that you can change the location of your study assets, or export-import a study into a different computer, and the study will still run without having to make any changes in the HTML code.  


1. Now it's time for a first glimpse: Click the '**Run**' button in either the study's or the component's toolbar. Your experiment should run like it did before without JATOS. Use the browser's developer tools to check for eventually missing files and other occurring errors.

### Edit your HTML and JavaScript

Up to this point JATOS served as a mere provider of your files. Now we want to use a feature of JATOS: We want to store your result data in JATOS' safe database. 

1. Include the **jatos.js** library in your HTML `<head>`

    Add the line `<script src="/assets/javascripts/jatos.js"></script>`

1. Add **`jatos.onload`**

   Every study in JATOS starts with this call. So whatever you want to do in your study it should start there.
   
   ~~~ javascript
   jatos.onLoad(function() {
     // initialize and start your JavaScript here 
   });
   ~~~
   
   E.g. if you want to initialize a jsPsych experiment:
   
   ~~~ javascript
   jatos.onLoad(function() {
     jsPsych.init( {
       ...
     });
   });
   ~~~
   
1. Now to actually send our result data to JATOS we use jatos.js' function **`jatos.submitResultData`**. We can pass this function any data in text format including JSON, CSV or XML.

   E.g. if we want to send a JavaScript object as JSON
   
   ~~~ javascript
   var resultJson = JSON.stringify(myObject);
   jatos.submitResultData(resultJson, jatos.startNextComponent);
   ~~~
    
   Conveniently but optionally `jatos.submitResultData` takes a second parameter which specifies what should be done after the result data got sent. Usually one want to jump to the next component (`jatos.startNextComponent`) or finish the study (`jatos.endStudy`).

   Another example where we use jsPsych: We have to put `jatos.submitResultData` into jsPsych's `on_finish`:
   
   ~~~ javascript
   jsPsych.init( {
     ...
     on_finish: function(data) {
       // Submit results to JATOS
       var resultJson = JSON.stringify(jsPsych.data.getData());
       jatos.submitResultData(resultJson, jatos.startNextComponent);
     }
   });
   ~~~

That's about it. Infos about other jatos.js functions and variables you can find in the [reference](jatos.js-Reference.html). 

### Beyond the basics

* Think about dividing your study into **several components**. You could have separate components e.g. for introduction, training, experiment and feedback. You could even consider splitting the experiment into several parts. One advantage is that if your participant stops in the middle of your study you still have the result data of the first components. Also, you can re-use components in different studies.
* Use the study's and component's '**JSON input data**'. With them you can change variables of your code directly through JATOS' GUI, which might come handy if someone isn't good in JavaScript.
* You can add a **quit button** to your study to allow the participant to [abort at any time](Data-Privacy-and-Ethics.html#things-you-should-consider-in-your-studies). 
