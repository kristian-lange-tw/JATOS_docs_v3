---
title: Manage Results
keywords: results, result data, data, files, result files, uploads, download, export, metadata
tags:
summary: The results pages (study, component, batch or worker) present all the data that were collected during the study runs, including the result data and metadata (e.g. worker ID, start time etc.). 
sidebar: mydoc_sidebar
permalink: Manage-Results.html
folder:
toc: true
last_updated: 3 Feb 2020
---

## Results Pages

Once you collected data for a study, you can see and manage the results by clicking on one of the *Results* buttons.

![Results Link](images/ResultsLink.png)

The image below is an example of a study results page, but there are result pages for components, batches or groups as well. There's quite a lot of information here, so we'll go through each piece.

![Results View screenshot](images/ResultsView-Screenshot1.png)


## Interacting With The Results Table

### View Result Data

Each study result has an arrow on the left. If you click on it, the result data for this study run will be displayed underneath the row. Since a study can have several components and each component produces its own result data there can be several result data each in its own row (like in the screenshot below).

![Results View screenshot](images/ResultsView-Screenshot3.png)


### Selecting Results

Prior to JATOS version 3.3.1 you could select/deselect a specific result by clicking anywhere on the row. Selected results change color to dark blue. 

From 3.3.1 on there is a checkbox on the left side of each row.

You can also use the buttons on the bar above to select/deselect all results in the table or select only all filtered ones.

![Results View screenshot](images/ResultsView-Screenshot2.png)


### Filter Results

The filter lets you search all all fields in the results table (the metadata) and from JATOS version 3.3.1 on also in the result data themselves. 

![Results View screenshot](images/ResultsView-Screenshot4.png)

If you type, for example, "Personal Single" in the *Filter Results* field, only the results ran by a Personal Single worker will appear on the table. You can then click on *Select Filtered* to select and then export only those results that you're interested in. 

For more eloborate filtering you can use Regular Expressions. Click on *RegEx* to active this.

By default filtering in case insensitive but you can turn on case sensitive filtering by clicking on *Aa*.


## Export

### Export Result Data

Once you selected the results you're interested in, click *Export Results* and *Selected* and you will download a text file that contains your results. Each line in this text file represents result data from one component. Alternatively you can also select *All* to get all result data.

![Results View screenshot](images/ResultsView-Screenshot6.png)

### Export Result Files (JATOS version >= 3.5.1)

Here you can download the result files that were uploaded during study runs. You can download single files by just clicking on them. Or similar to exporting result data select the lines you are interested in and download them with *Export Files* and *Selected*. Alternatively you can also select *All* to get all files.

![Results View screenshot](images/ResultsView-Screenshot5.png)

### Export Metadata (JATOS version >= 3.3.1)

Sometimes one is also interested in the metadata, that is what's in the actual table fields ("Result ID", "Start Time" , "Last Seen", ...). For this click on *Export Metadata* and the metadata of the selected results will be downloaded in CSV format.

![Results View screenshot](images/ResultsView-Screenshot7.png)


## Delete Results

You can click *Delete* to remove all or only some selected results (result data + result files + metadata). Keep in mind **there's no undo function for this**. 

![Results View screenshot](images/ResultsView-Screenshot8.png)


## Table Columns

You can show and hide the columns displayed in the table with the drop-down menu under the *Display Columns* button. 

![Results View screenshot](images/ResultsView-Screenshot9.png)

**Result ID** - An identifier assigned by JATOS to each study result. A study result is actually a set of component results, each of them with their own (different) *Component Result ID*. 

**Start Time** - Time (set at the server's time zone) at which the first component of the study was started. 

**End Time** - Time (set at the server's time zone) at which the last component of the study was finished. 

**Last Seen** - Each component running in a worker's browser sends a "heartbeat" regularly back to JATOS. Last Seen is the time of the last heartbeat received. The heartbeat stops either when the study is finished or when the browser tab is closed. The default period of the heartbeat is 2 minutes but you can change it through a [jatos.js function](jatos.js-Reference.html#jatossetheartbeatperiod).

**Duration** - Simply the time difference between the start and end time.

**Batch** - Name of the batch the worker belongs to.

**Worker ID** - Assigned by JATOS. Each worker has its own Worker ID. JATOS' admin user will always have Worker ID 1. You can click on a Worker ID to see all the worker's results. 

**Worker Type** - Displays the [Worker type](Worker-Types.html) that ran the study. 

**MTurk Worker ID (Confirmation Code)** - Only applies to studies run by MTurk workers. An identifier given by Amazon Mechanical Turk's, not by JATOS. The Confirmation Code is generated by JATOS and given to the worker as proof of his work.

**Group ID** - Only available for group studies. It identifies the group.

**Files** - Indicates result file upload

**State**

Possible states for study results are: 

* PRE - [Preview of study](Restricting-study-flow.html#preview-links) (exists only in PersonalSingleWorker and GeneralSingleWorker)
* STARTED - Study was started
* DATA_RETRIEVED - Study's jsonData were retrieved
* FINISHED - Study successfully finished
* ABORTED - Study aborted by worker
* FAIL - Something went wrong

Possible states for component results are:

* STARTED - Component was started
* DATA_RETRIEVED - Component's jsonData were retrieved
* RESULTDATA_POSTED - Result data were posted
* FINISHED - Component was finished
* RELOADED - Component was reloaded
* ABORTED - Component aborted by worker
* FAIL - Something went wrong

**Messages** - A message that can be set together with [jatos.endStudy](jatos.js-Reference.html#jatosendstudy) or [jatos.abortStudy](jatos.js-Reference.html#jatosabortstudy).
