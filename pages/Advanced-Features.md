---
title: Some Advanced Features
keywords: installation, advanced, JSON input, studyJsonInput, componentJsonInput
tags:
summary:
sidebar: mydoc_sidebar
permalink: Advanced-Features.html
folder:
toc: false
last_updated: 25 Sep 2020
---

## Study JSON Input and Component JSON Input

Sometimes you want to be able to quickly change your experiment's setup without changing the source code each time.

E.g. you want to 
* quickly change the introductory text
* change the number of trials
* update some parameters needed in the experiment

You can achieve this with the Study JSON Input or Component JSON Input. Both can be easily edited in the Study Properties or Component Properties.

![Study Properties / JSON input](images/Screenshot_studyJsonInput.png)

Both input fields take [JSON](https://www.w3schools.com/whatis/whatis_json.asp) and the data you put in there is then available in your study's JavaScript via `jatos.studyJsonInput` and `jatos.componentJsonInput`.

The difference between the Study JSON Input and Component JSON Input is that the first one is available during the whole study run, in all components, and the latter one only in the component for which it is specified.

**Example:**

If you put in the Study JSON Input

```javascript
{
   "introduction": "this is a text",
   "order": [3, 1, 2]
}
```

you can access those fields in your JavaScript with `jatos.studyJsonInput.introduction` and `jatos.studyJsonInput.order`.


## Study / Batch / Group Session

The sessions are there to help you exchange data within a study, batch or group. The Study Session allows to pass on data within the same study run, from one component to the next. With the Batch Session one can transfer data between study runs that belong to the same batch. There is a whole page dedicated to those sessions: [Session Data - Three Types](/Session-Data-Three-Types.html).


## Safe your result data

You probably want to safe the data that will be collected during your experiments. There are generally two ways to do this: 1) result data or 2) result files - and there is a [documentation page about it](Submit-and-upload-data-to-the-server.html).


## Group Studies

JATOS facilitates group studies in which participants can work together on the same experiment and exchange data in real-time.
To get an idea it's best to start with [examples](Example-Group-Studies.html), then one can go on to write them: [Write Group Studies I - Setup](Write-Group-Studies-I-Setup.html) and [Write Group Studies II - JavaScript and Messaging](Write-Group-Studies-II-JavaScript-and-Messaging.html).
