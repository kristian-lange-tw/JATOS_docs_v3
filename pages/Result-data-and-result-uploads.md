---
title: Result data and result uploads
keywords: results, result data, data, upload, download, result uploads, result files, files, jatos.uploadResultFile, jatos.downloadResultFile
tags:
summary:
sidebar: mydoc_sidebar
permalink: Result-data-and-result-uploads.html
folder:
toc: true
last_updated: 1 Feb 2020
---

We assume that you wrote your study with HTML/JavaScript/CSS or by using of the libraries. But now the data that is produced has to be sent to the JATOS server for safe storage and easy later retrieval. The first part is described here - the latter one in [Manage Results](Manage-Results.html).


### Submit result data

There are a couple of _jatos.js_ functions that allow you to send data to the JATOS server. The result data can be anything that can be put into text, that includes formats like JSON or CSV. Images, audio or video data are better suited for result files.

First there are [`jatos.submitResultData`](jatos.js-Reference.html#jatossubmitresultdata) and [`jatos.appendResultData`](jatos.js-Reference.html#jatosappendresultdata). The latter exists only since JATOS version 3.1.7. They do the same with the only difference that the first overwrites the data and therefor deletes previously sent data, while the latter appends the new data to the old data. 

Then there are a couple functions that do something else but allow the sending of result data out of convenience, since they usually go together anyway. These are all functions that start a new component (e.g. [`jatos.startNextComponent`](jatos.js-Reference.html#jatosstartnextcomponent), [`jatos.startComponentByPos`](jatos.js-Reference.html#jatosstartcomponentbypos)) and all functions that end a study ([`jatos.endStudy`](jatos.js-Reference.html#jatosendstudy) and [`jatos.endStudyAndRedirect`](jatos.js-Reference.html#jatosendstudyandredirect)). The latter one exists only since JATOS version 3.5.1 (prior versions can use [`jatos.endStudyAjax`](jatos.js-Reference.html#jatosendstudyajax)).


### Upload and download result files (Since JATOS version 3.5.1)

If you want to upload audio, video, images or any other data that is not in text format then uploading a result file is what you need: [`jatos.uploadResultFile`](jatos.js-Reference.html#jatossubmitresultdata). 

And if you want to, in a later component, access the uploaded files again you can download them with [`jatos.downloadResultFile`](jatos.js-Reference.html#jatosdownloadresultfile).

For more real-world examples have a look at the ['Drawing' and the 'Video Recording' examples](Example-Studies.html).
