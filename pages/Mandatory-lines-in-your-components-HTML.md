---
title: Mandatory lines in your components' HTML
keywords: mandatory, HTML, jatos.js
tags:
summary:
sidebar: mydoc_sidebar
permalink: Mandatory-lines-in-your-components-HTML.html
folder:
toc: true
last_updated: 28 Dec 2016
---

The best way to write an HTML/JavaScript file that runs with JATOS is to use one of the HTML files from the [Example Studies](http://www.jatos.org/Example-Studies.html) as a starting point.

Here are the absolute basics that any component HTML file MUST have in order to correctly run with JATOS

1. A link to the jatos.js library in the head section

   ~~~ html
   <html>
     <head>
       <script src="/assets/javascripts/jatos.js"></script>
     </head>
   </html>   
   ~~~

   [Remember](Troubleshooting.html#a-file-library-image--included-in-the-html-fails-to-load): Any URL or file path in a HTML file should only use '/' as a file path separator - even on Windows systems. 

1. A callback function that will execute after a component has finished loading

   ~~~ html
   <script>
     jatos.onLoad();
   </script>   
   ~~~

   The code above is valid, but your component will do nothing after being loaded, which is probably not what you want. Typically, you would define the function that would get your JavaScript going after component load. Something like this, for example, will show an alert box:

   ~~~ html
   <script>
     jatos.onLoad(function() {
       alert("I am an alert box!");
     });
   </script>
   ~~~


