---
title: Connect to Mechanical Turk
keywords: Mechanical Turk, MTurk, AMT, Amazon
tags:
summary:
sidebar: mydoc_sidebar
permalink: Connect-to-Mechanical-Turk.html
folder:
toc: false
last_updated: 28 Dec 2016
---

Connecting your JATOS study to the Mturk is easy, although a fair amount of clicking is required. 

You will need:
* A requester Mturk account
* Your study running on JATOS
* A description of the study (this can be the same as the one you included in the study description within JATOS)

The steps to create a project are part of the MTurk interface. 

1. Create --> New Project --> Other --> Create Project

1. Complete the 'Enter Properties' tab

1. Click on the 'Design layout' button in the bottom of the page. 

1. Click on the 'Source' button. You'll see some text in an editable window, corresponding to an html file. Delete the entire text in this field.

   ![MTurk Schreenshot](images/Screen Shot 2014-09-26 at 17.31.00.png)

1. In JATOS, go to the Study Toolbar ---> Batch Manager ---> Worker Setup ---> MTurk Worker row ---> Source Code.

   ![JATOS GUI screenshot](images/Screenshot from 2016-03-09 21:30:34.png){:width="200"}

1. You'll see a box with HTML code, similar to the one shown here. Copy paste the code from JATOS to the MTurk source section. 

   ![JATOS GUI screenshot](images/Screenshot from 2016-03-09 21:31:57.png)

1. Back in MTurk click on the 'Source' button again, and continue setting up your study in MTurk. 
 
   ![MTurk Schreenshot](images/Screen Shot 2014-09-26 at 17.06.17.png)

1. When an MTurk worker finishes a study they'll see a confirmation code. To assign payment to individual workers, just compare the confirmation codes stored in JATOS' results view to those stored in MTurk.

   ![Confirmation code](images/Screenshot from 2015-04-09 15_17_03.png){:height="100"}

See the [Tips & Tricks](Tips-and-Tricks.html) page for some useful information on how to test your study before officially posting it on MTurk. 
