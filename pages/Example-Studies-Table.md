---
title: Example Studies Table
keywords: example studies, jspsych
tags:
summary: Tabulated list of example studies 
sidebar: mydoc_sidebar
permalink: Example-Studies-Table.html
folder:
toc: true
last_updated: 05 May 2019
---

### Overview
JATOS gives you complete freedom on the client side. You can do whatever you like! But these examples might help as a starting point. We tried to have at least one example to illustrate each of JATOS' main features. 

| Study Name             | Brief description   | Frameworks used | Features used   | Example image  |
|-------------------|-------------------|-------------------|-------------------|-------------------|
| [Hello World](https://github.com/JATOS/JATOS_examples/raw/master/examples/hello_world.zip) | Everything starts with a Hello World! | None | None | None  |
| [Go-/No-Go Task](https://github.com/JATOS/JATOS_examples/raw/master/examples/go-nogo_task_(using_jspsych_6).zip) | Go/NoGo task. Includes instructions | jsPsych | None |  ![dummy](images/example-studies/Screenshot_gonogo.png){:width="50"}|
| [Randomize Tasks Between Workers](https://github.com/JATOS/JATOS_examples/raw/master/examples/randomize_tasks_between_workers.zip)§| Template to randomly assign participants to conditions A, B, or C (with fixed numbers for each condition) | None | Batch session| {% include image.html file="example-studies/Screenshot_randomization_between_workers.png" alt="Screenshot Randomization between participants" max-width="200" %} |
| [Lexical Decision Making](https://github.com/JATOS/JATOS_examples/raw/master/examples/lexical_decision_(using_jspsych).zip) | Participants classify whether a string of letters is a word or a nonword. Taken from [http://www.factorsdb.org/](http://www.factorsdb.org/). | jsPsych | None | {% include image.html file="example-studies/Screenshot_lexicalDecision_word.png" alt="Screenshot Lexical Decision" max-width="200" %} |
| [Random Dot Kinematogram](https://github.com/JATOS/JATOS_examples/raw/master/examples/rdk.zip)§ | A random dot kinematogram (RDK) for online visual psychophysics and the use in web browsers. By _Sivananda Rajananda, Hakwan Lau, Brian Odegaard_ ([preprint](https://www.biorxiv.org/content/early/2017/09/21/192377)) | jsPsych | no feature| {% include image.html file="example-studies/Screenshot_rdk.png" alt="Screenshot RDK" max-width="200" %} |
| [Demographic and Survey questions](https://github.com/JATOS/JATOS_examples/raw/master/examples/survey.js_ui_example.zip) | [SurveyJS](http://surveyjs.org) is an easy to use library to create simple forms or complex surveys and questionaires. Have a look at [surveyjs.org/examples/jquery/questiontype-text](http://surveyjs.org/examples/jquery/questiontype-text/) to see what's possible. | SurveyJS | no feature| {% include image.html file="example-studies/survey-js-screenshot.png" alt="Screenshot SurveyJS Example" max-width="200" %} |
| [Instruction with Google Slides](https://github.com/JATOS/JATOS_examples/raw/master/examples/intro_with_google_slides.zip)§ | Use Google Slides to make an quick, easy and versatile instruction page. Might not be the prettiest, but it does the job| no frameowrk | no feature| {% include image.html file="example-studies/Screenshot_intro_slides.png" alt="Screenshot Easy instructions with Slides" max-width="200" %}|
| [p5.js](https://github.com/JATOS/JATOS_examples/raw/master/examples/p5.js_examples.zip)§ | [p5.js](https://p5js.org/) is a graphics library to easily create 2D and 3D graphics without deeper knowledge of how those graphics are rendered. Additionally one can add user interaction, video, sound, or capture from the webcam or the mic. Have a look at their [example section](https://p5js.org/examples/). | p5 | no feature| {% include image.html file="example-studies/p5-js-screenshot5.gif" alt="Screenshot p5.js Example" max-width="200" %}|



§ Requires JATOS version 3.1.1 or newer
