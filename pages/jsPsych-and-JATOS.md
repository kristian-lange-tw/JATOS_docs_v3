---
title: jsPsych and JATOS
keywords: jsPsych
tags:
summary:
sidebar: mydoc_sidebar
permalink: jsPsych-and-JATOS.html
folder:
toc: true
last_updated: 29 Dec 2016
---

JATOS basically cares for the server side: it stores result data, does worker management etc. JATOS doesn't care so much for what happens in the browser itself - your HTML, JavaScript and CSS. Of course you can write this all yourself, but you could also use a framework for this. A very good one is [jsPsych](http://www.jspsych.org/).

In [our example studies](http://www.jatos.org/Example-Studies.html) are a couple of jsPsych ones.

Here are the necessary changes if you want to adapt your jsPsych experiment so that it runs within (and send the result data to) JATOS. Additionally you can have a look at [Adapt Pre written Code to run it in JATOS (Jatosify)](Adapt-Pre-written-Code-to-run-it-in-JATOS.html).

### How to turn your jsPsych experiment into a JATOS study

1. Include the `jatos.js` library in the `<head>`

   ~~~ html
   <script src="/assets/javascripts/jatos.js"></script>
   ~~~ 
   
   [Remember](Troubleshooting.html#a-file-library-image--included-in-the-html-fails-to-load): Any URL or file path in a HTML file should only use '/' as a file path separator - even on Windows systems. 

1. Wrap jsPsych's init call `jsPsych.init` in a `jatos.onload` call

   ~~~ javascript
   jatos.onload(function() {
     jsPsych.init( {
       // ...
     });
   });
   ~~~
   
That's all. If you additionally want to send your result data to JATOS read on.

### Send jsPsych's result data back to JATOS

Here we use jsPsych's function `jsPsych.data.getData()` to collect the data into a variable and then 'stringify' the JSON format into a simple string.
Then we use JATOS' function `jatos.submitResultData` to send your result to JATOS and asks JATOS to move to the next component, if there is one.

~~~ javascript
jatos.onload(function() {
  jsPsych.init( {
    // ...
    on_finish: function() {
      var resultJson = JSON.stringify(jsPsych.data.getData());
      jatos.submitResultData(resultJson, jatos.startNextComponent);
    }
  });
});
~~~ 
