---
title: Run Longitudinal Studies on Prolific
keywords: Longitudinal, Prolific, Batch Session, Worker Links
tags:
summary:
sidebar: mydoc_sidebar
permalink: Running-longitudinal-studies-on-Prolific.html
folder:
toc: false
last_updated: 5 Feb 2020
---


Prolific [says](https://researcher-help.prolific.co/hc/en-gb/articles/360009222733-Longitudinal-Multi-part-studies) that to run a study longitudinally you need to set up one study per session. That's the easy part. Simply set the same external URL on all the individual studies. 

There are two things you need to care from in your JavaScript: 

1. Make sure that you record the Prolific ID. In the Study Settings in Prolific, enable the option to include special query parameters in the URL. 
![Prolific Screenshot](images/Screenshot_ExtendURL_Prolific.png)   

You can configure their names here

![Prolific Screenshot](images/Screenshot_useExtendedURL_prolific.png)   

If you select these options in Prolific, you'll be able to collect the Prolific ID from your JavaScript by using the *jatos.js* object `ID = jatos.urlQueryParameters.PROLIFIC_PID;` 

(If you've cheanged the name of the `PROLIFIC_ID` quesry parameter in Prolific, you'll have to change it accordingly on your JS. 
