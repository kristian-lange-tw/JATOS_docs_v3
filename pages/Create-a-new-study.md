---
title: Create a new study
keywords: create, import, export
tags:
summary:
sidebar: mydoc_sidebar
permalink: Create-a-new-study.html
folder:
toc: true
last_updated: 24 Nov 2019
---

There are two ways to create a new study: by modifying an existing one from our examples, or by creating one from scratch. 

**Developement of a JATOS study usually happens on your local JATOS: [Run an experiment with JATOS - Workflow](Run-an-experiment-with-JATOS-Workflow.html)**

### Modify an existing study

Take an existing study (e.g. from [Example Studies](Example-Studies.html)) as a prototype and modify it bit by bit. We recommend you start with this to get a quick idea of how JATOS works. Just import an existing study and clone it by clicking on More → Clone in the study bar.

### Write your own study from scratch

Press the **New Study** button in the header of your local JATOS. Then edit the study properties and add new components manually. You will have to write your own JavaScript code. 

The most difficult part - though it's still easy! - is to learn to write your own study component scripts, using HTML, CSS and JavaScripts. Or, instead of reinventing the wheel, you could use a framework like [jsPsych](jsPsych-and-JATOS.html), [OSWeb](OSWeb-and-JATOS.html) or [lab.js](labjs-and-JATOS.html).

Check out the [Mandatory lines in your components' HTML](Mandatory-lines-in-your-components-HTML.html) page to know what you absolutely must include in your scripts in order to let JATOS see them. Also check out the [jatos.js Reference](jatos.js-Reference.html), that contains a set of very useful functions that you have to use to communicate with jatos (to e.g. submit and receive data).

If you are a newbie to HTML/JavaScript programming, there are many free and excellent tutorials online. Like [this one from the Kahn Academy](https://www.khanacademy.org/computing/computer-programming) or more searchable tutorials like the simple ones from the [w3 schools](http://www.w3schools.com/). In addition, [StackOverflow](http://stackoverflow.com/questions/tagged/html) is the best place to solve the problems that hundreds of others have encountered before.  

