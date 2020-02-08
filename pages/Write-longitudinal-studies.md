---
title: Write longitudinal studies
keywords: longitudinal, batch session
tags:
summary:
sidebar: mydoc_sidebar
permalink: Write-longitudinal-studies.html
folder:
toc: false
last_updated: 5 Feb 2020
---


# Write longitudinal studies
You might want to collect data from the same participant multiple times and, crucially, be able to link the multiple result data from a single participant. There are several options for this, and your exact solution may depend on how you are recruiting participants. Here's one way in which you could do it:

## Use the batch session data to store results that outlive a study run

Whenever a participant clicks on a study link, JATOS internally starts a study run. Once the data from the last component are sumitted, the study run is finished and the data are no longer avalable to the client side. So, to run a longitudinal study, you need store data in a way that outlives the particular study run and is avalable to future runs. The [Batch session data](Session-Data-Three-Types.html) does just this.  

# Example

## Assign an ID to individual workers

The first thing you need to do is make sure that the same *person* is assigned a single, unique ID. Several options are possible:
1. If your sample size is relatively small and you can afford it, you could send individualized [Personal Multiple links](Worker-Types.html#-personal-multiple-worker) to each participant. If a worker runs a study with this link, JATOS will assign them a unique number. You can access MTurk's worker ID in your JavaScript through `jatos.urlQueryParameters.workerId` from the _jatos.js_ library.
2. If you are recruiting participants through a marketplace, like MTurk or Prolific, you can simply use the marketplace worker ID. 
It's straightforward in MTurk: You can access the worker ID in your JavaScript through `jatos.urlQueryParameters.workerId`.
For Prolific, it's a bit more complicated. See [running longitudinal studies in Prolific](Running-longitudinal-studies-on-Prolific.html) for detailed instructions.
3. If neither of these are true, and you want a large sample of participants recruited outside of a marketplace (i.e. if you are using a [General Multiple link](Worker-Types.html#-general-multiple-worker), you could provide each new participant with a unique ID that they then have to store and provide (manually) in the following session. Note that, when a participant runs a study with a General Single JATOS stores cookies on their browser to prevent them from taking part twice in the same study. But these cookies are minimal and not intended to be used to identify participants or to link a browser to any given result data. 


## Store bits of result data that are necessary for future sessions

Once you have an ID, you should assign to it the information relevant for the following sessions in your longitudinal study. Say you need to store the number of correct responses for a given session. You could do it with the command:

``` 
var performanceInfo = {"percentageCorrect" : nCorrect/nTrials, "nTrials" : nTrials}
jatos.batchSession.add("/subjects/" + ID, performanceInfo); 
```

Which will append the information from `ID` and `percentageCorrect` to the already existing Batch session data and give you something that looks (e.g.) like this in the Batch session: 

```
{
  "subjects": {
    "MyemLF": {
      "percentCorrect": 62,
      "nTrials" : 250
    },
    "74b61m": {
      "percentCorrect": 78,
      "nTrials" : 250
    },
    "pFyxRT": {
      "percentCorrect": 67,
      "nTrials" : 247
    }
}
```


**Note that the information stored in the Batch Session is visible to the client side, so it should contain only the strictly necessary, pseudonymized data.** In other words, store only summary data like the condition assigned (read [more](Between-subjects-designs.html) on randomizing conditions between participants) number of trials completed or correct, etc. But nothing else.


## Recover the corresponding bit of the result data from the Batch Session

You could do that with the following command: 

`subjsPreviousPerformance = jatos.batchSession.getAll().subjects[ID]`

That's it. Once you have your worker's ID and the corresponding longitudinally-relevant data, you can use it as a starting point for your next session. 


