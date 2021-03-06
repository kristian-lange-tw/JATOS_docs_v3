---
title: Example Studies
keywords: examples, jspsych, javascript, bootstrap, jquery, pure, css, highchart, survey
tags:
summary: These examples here are mainly a showcase for what JATOS can do for you while you are writing your studies (like easy import/export, safe results storing and presentation, messaging in group studies). They are not meant to show what JATOS itself does (since JATOS doesn't care for the browser side).
sidebar: mydoc_sidebar
permalink: Example-Studies.html
folder:
toc: true
last_updated: 3 Oct 2017
---

If you wrote an example study that you'd like to share, please feel free to [contact us](Contact-us.html) and we'll include it in this page!

Since JATOS cares mostly for the server side it gives you the freedom to use in your study code whatever technologies work in browsers (e.g. HTML5 canvas, CSS3 or 3D graphics with WebGL). Additionally browser-side JavaScript libraries or frameworks like [jQuery](https://jquery.com/), [AngularJS](https://angularjs.org/), [Bootstrap](http://getbootstrap.com/), [Highcharts](http://www.highcharts.com/), [p5](https://p5js.org/), or [jsPsych](http://www.jspsych.org/) are possible and will smooth out your path to quick and easy development. Of course the same is true for CSS modules (e.g. [Pure.css](http://purecss.io/), [Material Design](http://www.google.com/design/spec/material-design/introduction.html)).

You can easily import/export study in JATOS. There is an 'Import Study' button in the header of each page and each study has an 'Export Study' button hidden under the 'More' button.

Another library of examples of psychological experiments is the [Experiment Factory](https://expfactory.github.io/table.html). All those experiments are easily jatosifyable - like we did with the [Self Regulation Survey](#self-regulation-survey-from-the-experiment-factory).

<b>If you have trouble downloading a study (common in Safari browsers) check [this troubleshooting tip](Troubleshooting.html#downloading-a-study--exporting-a-study-fails-eg-in-safari-browsers).</b>

### Hello World Example

Everything starts with a Hello World!

[Download Hello World example](https://github.com/JATOS/JATOS_examples/raw/master/examples/hello_world.zip).

### Go- / No-Go Task (with jsPsych 5.0.3)

Standard Go- / No-Go experiment.
This study illustrates the compatibility between JATOS and the excellent **jsPsych** library ([www.jspsych.org](http://www.jspsych.org/)). With jsPsych one can program the actual experiment while JATOS cares for the server-side.

![Screenshot Go- / No-Go Task](images/example-studies/Screenshot_gonogo.png){:width="300"}

**Needs JATOS version 2.1.7 or newer**

[Download Go-/No-Go Task](https://github.com/JATOS/JATOS_examples/raw/master/examples/go-nogo_task_(using_jspsych).zip)

### Randomize conditions between participants (Go- / No-Go Task)

Standard Go- / No-Go experiment with two different conditions. Half of the participants are assigned to condition A, the other half to condition B. Uses the Batch Session. 

![Screenshot Go- / No-Go Task](images/example-studies/Screenshot_gonogo.png){:width="300"}

**Needs JATOS version 3.1.1 or newer**

[Download Randomization with Go-/No-Go Task](https://github.com/JATOS/JATOS_examples/raw/master/examples/go-no-go_task_(randomize_between_workers).zip)

### Lexical Decision (with jsPsych 5.0.3)

Taken from [http://www.factorsdb.org/](http://www.factorsdb.org/) using **jsPsych** library ([www.jspsych.org](http://www.jspsych.org/))
> In a lexical decision task, participants classify whether a string of letters is a word or a nonword. This version is based on one of the earliest lexical decision tasks, reported in Rubenstein, Garfield, & Millikan, 1970. The experiment tests response time for high and low frequency English words.

![Screenshot Lexical Decision](images/example-studies/Screenshot_lexicalDecision_word.png){:width="300"}

**Needs JATOS version 2.1.7 or newer**

[Download Lexical Decision](https://github.com/JATOS/JATOS_examples/raw/master/examples/lexical_decision_(using_jspsych).zip)

### Random Dot Kinematogram (with jsPsych 5.0.3)

By _Sivananda Rajananda, Hakwan Lau, Brian Odegaard_ ([preprint](https://www.biorxiv.org/content/early/2017/09/21/192377))

Source code: [github.com/vrsivananda/RDK](https://github.com/vrsivananda/RDK)

A random dot kinematogram (RDK) for online visual psychophysics and the use in web browsers. 

> This fully-customizable RDK offers options to implement several different types of noise (random position, random walk, random direction) and parameters to control aperture shape, coherence level, the number of dots, and many other features.

![Screenshot RDK](images/example-studies/Screenshot_rdk.png){:width="300"}

**Needs JATOS version 3.1.1 or newer**

[Download RDK Example](https://github.com/JATOS/JATOS_examples/raw/master/examples/rdk.zip)

### Demographic and Survey questions (using SurveyJS library)

[SurveyJS](http://surveyjs.org) is an easy to use library to create simple forms or complex surveys and questionaires. Have a look at [surveyjs.org/examples/jquery/questiontype-text](http://surveyjs.org/examples/jquery/questiontype-text/) to see what is possible.

![Screenshot SurveyJS Example](images/example-studies/survey-js-screenshot.png){:width="300"}

**Needs JATOS version 3.1.1 or newer**

[Download SurveyJS Example](https://github.com/JATOS/JATOS_examples/raw/master/examples/survey.js_ui_example.zip)

### jQuery UI Example

With [jQuery UI](https://jqueryui.com/) it's quite simple to add common (and pretty!) GUI elements to your study, like a date picker, a sortable list or a slider.

![Screenshot jQuery UI Example](images/example-studies/Screenshot_jqueryuiExample_personalData.png){:width="300"}

**Needs JATOS version 2.1.7 or newer**

[Download jQuery UI Example Study](https://github.com/JATOS/JATOS_examples/raw/master/examples/jquery_ui_example_study.zip)

### Interactive 2D/3D Graphics (with p5.js library)

[p5.js](https://p5js.org/) is a graphics library to easily create 2D and 3D graphics without deeper knowledge of how those graphics are rendered. Additionally one can add user interaction, video, sound, or capture from the webcam or the mic. Have a look at their [example section](https://p5js.org/examples/).

![Screenshot p5.js Example](images/example-studies/p5-js-screenshot5.gif){:width="300"}

**Needs JATOS version 3.1.1 or newer**

[Download p5.js Example](https://github.com/JATOS/JATOS_examples/raw/master/examples/p5.js_examples.zip)

### Video Example

Shows how to embed a video with HTML 5 by using the browsers video player, YouTube, or the [video.js](http://www.videojs.com/) JavaScript library.

![Screenshot Video Example](images/example-studies/Screenshot_videoExample2.png){:width="300"}

**Needs JATOS version 1.1.11 or newer**

[Download Video Example study](https://github.com/JATOS/JATOS_examples/raw/master/examples/video_example_study.zip)

### Results in CSV Format Example

Simple example of how to store results in CSV format

![Screenshot Results in CSV Format Example](images/example-studies/Screenshot_csv_example.png){:width="300"}

**Needs JATOS version 2.1.7 or newer**

[Download Results as CSV Example](https://github.com/JATOS/JATOS_examples/raw/master/examples/results_as_csv_example.zip)

### Simple Consent Form

Simple example of a consent form with text and buttons 'I agree' and 'Cancel'.

![Screenshot Simple Consent Form](images/example-studies/Screenshot_consent_form.png){:width="300"}

**Needs JATOS version 2.1.7 or newer**

[Download Consent Form](https://github.com/JATOS/JATOS_examples/raw/master/examples/consent_form.zip)

### Consent Form and Introduction with Preview Feature

This mobile-friendly example just has an introduction component that includes a consent text. With pressing the start button the worker gives his consent. This is also a good showcase for the [JATOS' preview feature](Worker-Types.html#preview-links). 

![Screenshot Preview Showcase (Introduction with Consent)](images/example-studies/Screenshot_preview_showcase.png){:width="300"}

**Needs JATOS version 2.1.7 or newer**

[Download Consent Form and Introduction with Preview Feature](https://github.com/JATOS/JATOS_examples/raw/master/examples/consent_form_and_introduction_with_preview_feature.zip)


### 2048 Game

This addictive game is created by Gabriele Cirulli. Based on 1024 by Veewo Studio and conceptually similar to Threes by Asher Vollmer. The original game is published under the MIT licence. The source code can be found in [GitHub](https://github.com/gabrielecirulli/2048). 

![Screenshot 2048 Game](images/example-studies/Screenshot_2048Game.png){:width="300"}

**Needs JATOS version 1.1.11 or newer**

[Download 2048 game](https://github.com/JATOS/JATOS_examples/raw/master/examples/2048.zip)

### Data Visualization Example (with Highcharts)

An example of a (slightly different) use of JATOS. Here, we're not collecting participants' data. We're just using JATOS as a regular server to display an HTML page. In this case, the page uses the [Highcharts library](http://www.highcharts.com/) to  display the results from a questionnaire that we ran online in JATOS.

![Screenshot Data Visualization Example (with Highcharts)](images/example-studies/Screenshot_dataDisplay_scatter.png){:width="300"}

**Needs JATOS version 1.1.11 or newer**

[Download Data Visualization example](https://github.com/JATOS/JATOS_examples/raw/master/examples/data_visualization_-_example.zip)

### Angling Risk Task Always Sunny (using jsPsych)

This is a study using **jsPsych** library ([www.jspsych.org](http://www.jspsych.org/)) taken from [expfactory.github.io](http://expfactory.github.io/). It's another example for how easy it is to use JATOS as a backend for jsPsych. 

> In this task, you will participate in a fishing tournament. During this tournament you will play a fishing game for multiple rounds. Each round, you will see a lake which has many fish in it. Your goal is to catch as many fish as possible.

![Screenshot Angling Risk Task Always Sunny](images/example-studies/Screenshot_anglingTask.png){:width="300"}

**Needs JATOS version 2.1.7 or newer**

[Download Angling Risk Task Always Sunny](https://github.com/JATOS/JATOS_examples/raw/master/examples/angling_risk_task_always_sunny.zip)

### Self Regulation Survey (from The Experiment Factory)

This is an example for standard questionnaire as done by [expfactory.github.io](http://expfactory.github.io/).

![Screenshot Self Regulation Survey](images/example-studies/Screenshot_selfRegulationSurvey.png){:width="300"}

**Needs JATOS version 2.1.7 or newer**

[Download Self Regulation Survey](https://github.com/JATOS/JATOS_examples/raw/master/examples/self_regulation_survey.zip)

### Invaders Game (with Phaser framework)

This classical arcade game is an example for a game made with the Phaser framework ([phaser.io](http://phaser.io/)). It is taken from their examples at [github.com/photonstorm/phaser-examples](https://github.com/photonstorm/phaser-examples).

![Screenshot Invaders Game (with Phaser framework)](images/example-studies/Screenshot_spaceInvaders.png){:width="300"}

**Needs JATOS version 2.1.7 or newer**

[Download Invaders Game](https://github.com/JATOS/JATOS_examples/raw/master/examples/invaders_with_phaser.zip)

### Perceptual Metacognition (using jsPsych)

This is a standard visual metacognition task. It is uses the **jsPsych** library ([www.jspsych.org](http://www.jspsych.org/)) and is taken from [expfactory.github.io](http://expfactory.github.io/).

![Screenshot Perceptual Metacognition](images/example-studies/Screenshot_perceptional_metacognition_stumili.png){:width="300"}

**Needs JATOS version 2.1.7 or newer**

[Download Perceptual Metacognition Study](https://github.com/JATOS/JATOS_examples/raw/master/examples/perceptual_metacognition_(jatosified).zip)

### Potato Compass (using interact.js)

Example how to use [interact.js](http://interactjs.io/) to achieve draggable elements (drag & drop).

![Screenshot Potato Compass (using interact.js)](images/example-studies/Screenshot_potatoCompass.png){:width="300"}

**Needs JATOS version 2.1.7 or newer**

[Download Potato Compass Study](https://github.com/JATOS/JATOS_examples/raw/master/examples/potato_compass.zip)

### Study, Group, and Batch Session Example Study

In this example we show JATOS' three different session types in action (see [Session Data - Three Types](Session-Data-Three-Types.html) for more information).

![Screenshot Study, Group, and Batch Session Example Study](images/example-studies/ChatExample_4.png){:width="300"}

**Needs JATOS version 3.1.1 or newer**

[Download Study, Group, and Batch Session example](https://github.com/JATOS/JATOS_examples/raw/master/examples/study__group__and_batch_session.zip)

### Group Chat

Let members of a group study talk to each other: Here is a chat example. It uses the Group Session. 

![Screenshot Group Chat](images/example-studies/Screenshot_chat.png){:width="300"}

**Needs JATOS version 3.1.1 or newer**

[Download Group Chat example](https://github.com/JATOS/JATOS_examples/raw/master/examples/group_chat.zip)

### Batch Chat

Let members of a batch talk to each other: Here is a chat example. It uses the Batch Session. 

![Screenshot Group Chat](images/example-studies/Screenshot_chat.png){:width="300"}

**Needs JATOS version 3.1.1 or newer**

[Download Batch Chat example](https://github.com/JATOS/JATOS_examples/raw/master/examples/batch_chat.zip)

### Prisoner's Dilemma

This is an implementation of the [Prisoner's Dilemma](https://en.wikipedia.org/wiki/Prisoner%27s_dilemma) to show the group study feature of JATOS where two workers interact with each other in the same study run.

![Screenshot Prisoner's Dilemma](images/example-studies/Screenshot_prisonersDilemma.png){:width="300"}

**Needs JATOS version 3.1.1 or newer**

[Download Prisoner's Dilemma example](https://github.com/JATOS/JATOS_examples/raw/master/examples/prisoner's_dilemma.zip)

### Snake

This is a variant of the [Snake game](https://en.wikipedia.org/wiki/Snake_(video_game)) in which one can play against several other players to show the group study feature of JATOS where several workers interact with each other in the same study run.

![Screenshot Snake](images/example-studies/Screenshot_snakeGame.png){:width="300"}

**Needs JATOS version 2.1.3 or newer**

[Download Snake Game example](https://github.com/JATOS/JATOS_examples/raw/master/examples/snake_game.zip)


