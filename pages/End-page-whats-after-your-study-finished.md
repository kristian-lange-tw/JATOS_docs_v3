---
title: End page - what's after your study finished
keywords: endPage, redirect, end, finish, endStudyAndRedirect
tags:
summary:
sidebar: mydoc_sidebar
permalink: End-page-whats-after-your-study-finished.html
folder:
toc: true
last_updated: 30 Jan 2020
---

### 1. Default

By default JATOS just shows the text "**This study is finished. Thank you for your participation.**" in English language after a study finshed. Maybe you want a different language or add a logo and different text then read on.


### 2. endPage.html (since JATOS v3.5.1)

You can put a file named '_endPage.html_' in your study assets folder along with your other study's file. JATOS will automatically redirect to this page if it exists.

**Hint 1:** But be aware that you cannot load or use any other files from the study assets folder. Since the study is already finished JATOS won't allow you accessing any other file from this folder, nor any of the JATOS sessions (study, batch and group) out of security reasons. Of course this doesn't prevent you from loading images or libraries (or any other resource) directly from the internet.

**Hint 2:** The _endPage.html_ won't be shown if the **MT Worker** (Worker for MTurk) is used. This has the simple reason that the MT Worker has to be redirected to the page that shows the confirmation code (they need it to claim their money). Similarily if you run your study with the **JATOS GUI** it won't show you the _endPage.html_ but redirects you back to JATOS' GUI.


### 4. Study Properties' End Redirect URL (since JATOS v3.5.1)

But maybe you want to redirect to a different page, e.g. a Prolific's end page or your department's calender? This you can do by putting the URL of that page into the study properties in JATOS GUI. 

![screenshot](images/Screenshot_end-redirect-url.png)


### 3. jatos.endStudyAndRedirect (since JATOS v3.5.1) or jatos.endStudyAjax (all JATOS versions)

Maybe the page to be redirected is determined only during the study run. Here you can use one of the two _jatos.js_ functions [`jatos.endStudyAndRedirect`](jatos.js-Reference.html#jatosendstudyandredirect) or [`jatos.endStudyAjax`](jatos.js-Reference.html#jatosendstudyajax) in the JavaScript of your study's **last component**. This is the most versatile way.
