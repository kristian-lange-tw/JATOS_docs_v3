---
title: Connect to Mechanical Turk
keywords: Mechanical Turk, MTurk, AMT, Amazon, Sandbox
tags:
summary:
sidebar: mydoc_sidebar
permalink: Connect-to-Mechanical-Turk.html
folder:
toc: false
last_updated: 24 Nov 2019
---

Connecting your JATOS study to the Mturk is easy, although a fair amount of clicking is required.

A good idea is always to try it yourself first in **MTurk Sandbox** before you let real workers do it.

### You will need

* A requester Mturk account
* Your study running on a [JATOS server](Bring-your-JATOS-online.html)
* A description of the study (this can be the same as the one you included in the study description within JATOS)


### On JATOS page

In JATOS, go to the Study Toolbar ⟶ Worker & Batch Manager

![JATOS GUI screenshot](images/worker-batch-manager-mturk.png)

1. Open the Worker Setup of the batch you want to run

1. Enable the MTurk worker type

1. Click on *Source Code*. You'll see a box with HTML code, similar to the one shown here. You will have to copy and paste the code from here to the MTurk interface.

   ![JATOS GUI screenshot](images/worker-batch-manager-mturk-source-code.png)


### On MTurk's page

You first have to create a project in the MTurk interface:

1. Create ⟶ New Project ⟶ Survey Link ⟶ Create Project

1. Complete the *Enter Properties* tab

1. Click on the *Design layout* button in the bottom of the page. 

1. Click on the *Source* button. You'll see some text in an editable window, corresponding to an HTML file. Delete the entire text in this field.

   ![MTurk Schreenshot](images/MTurk-source-editor.png)   

1. Now paste the source code that you got from JATOS into this text field. This HTML code works out-of-the-box and you don't have to change anything (but you can if you want).
 
1. To exit the editing mode, click on the ‘Source’ button again and continue setting up your study in MTurk.
 
   ![MTurk Schreenshot](images/MTurk-source-editor-done.png)


### What should happen

When an MTurk worker finishes a study they'll see a confirmation code. To assign payment to individual workers, just compare the confirmation codes stored in JATOS' results view to those stored in MTurk.

   ![Confirmation code](images/MTurk-confirmation-code.png)

