---
title: Mandatory lines in your components' HTML
keywords: mandatory, HTML, jatos.js
tags:
summary:
sidebar: mydoc_sidebar
permalink: Mandatory-lines-in-your-components-HTML.html
folder:
toc: true
last_updated: 28 Jan 2020
---

The best way to write an HTML/JavaScript file that runs with JATOS is to use one of the HTML files from the [Example Studies](Example-Studies.html) as a starting point.

Here are the absolute basics that any component HTML file must have in order to correctly run with JATOS

1. A link to the jatos.js library in the head section

   ~~~ html
   <html>
     <head>
       <script src="/assets/javascripts/jatos.js"></script>
     </head>
   </html>   
   ~~~

   Since JATOS v3.3.1 it can be simplified:

   ~~~ html
   <html>
     <head>
       <script src="jatos.js"></script>
     </head>
   </html>   
   ~~~

   [Remember](Troubleshooting.html#a-file-library-image--included-in-the-html-fails-to-load): Any URL or file path in a HTML file should only use `/` as a file path separator - even on Windows systems. 

1. The second bit is not really necessary but without defining the `jatos.onLoad` callback function you won't be able to use jatos.js' features. Of course you could start right away with any JavaScript but if you want to use jatos.js' variables and functions you have to wait untill it is finished initializing. This initialization includes among others setting up the study and component JSON input variables and the study, batch, and group sessions. If you try to access one of jatos.js variables or functions before the initialization is finished it might lead to an error or wrong results.

   ~~~ html
   <script>
     jatos.onLoad(function() {
       // Start here with your code that uses jatos.js' variables and functions
     });
   </script>   
   ~~~



