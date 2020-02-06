---
title: End page - After your study finished
keywords: endPage, redirect, end, finish, endStudyAndRedirect
tags:
summary:
sidebar: mydoc_sidebar
permalink: End-page-after-your-study-finished.html
folder:
toc: true
last_updated: 5 Feb 2020
---

### 1. Default

By default JATOS just shows the text "**This study is finished. Thank you for your participation.**" in English language, with no special formatting, after a study finshed. Maybe you want a different language or add a logo and different text or styling, then read on.


### 2. endPage.html (since JATOS v3.5.1)

If you include a file named '_endPage.html_' in your study assets folder along with your other study's files, JATOS will automatically redirect to this page after the study finished.

**Hint 1:** Be aware that in the '_endPage.html_' you cannot load or use any other files from the study assets folder. Because the study is already finished, JATOS won't allow you to access any other file from this folder, or from any of the JATOS sessions (study, batch and group) out of security reasons. Of course this doesn't prevent you from loading images or libraries (or any other resource) directly from the internet.

**Hint 2:** If you run the study with an **MT Worker** (Worker for MTurk) then you probably want to show the confirmation code to your worker. This is passed on to the _endPage.html_ in a cookie with the name *JATOS_CONFIRMATION_CODE*.

**Hint 3:** If you run your study with the **JATOS GUI** it won't show you the _endPage.html_ but redirect you back to JATOS' GUI instead.


### 3. Study Properties' End Redirect URL (since JATOS v3.5.1)

Maybe you want to redirect to a different page, e.g. a Prolific's end page or your department's webpage. This you can do by putting the URL of that page into the study properties in JATOS' GUI. 

![screenshot](images/Screenshot_end-redirect-url.png)

**Hint:** If you run the study with an **MT Worker** (Worker for MTurk) then you probably want to show the confirmation code to your worker. This is passed on as an URL query parameter *confirmationCode*.


### 4. `jatos.endStudyAndRedirect` (since JATOS v3.5.1) or `jatos.endStudyAjax` (all JATOS versions)

If you want to determine dynamically (i.e. in the JavaScript) the address of the webpage that your participants see after finishing a study, you can use one of the two _jatos.js_ functions [`jatos.endStudyAndRedirect`](jatos.js-Reference.html#jatosendstudyandredirect) or [`jatos.endStudyAjax`](jatos.js-Reference.html#jatosendstudyajax) in the JavaScript of your study's **last component**. This is the most versatile way.
