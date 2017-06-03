---
title: Session Data - Three Types
keywords: session data, study session, group session, batch session
tags:
summary:
sidebar: mydoc_sidebar
permalink: Session-Data-Three-Types.html
folder:
toc: false
last_updated: 2 June 2017
---

Often you want to store information during a study run and share it with other components of the same study, or between workers of a group or batch. For this purpose, use one of the three different session types available.

Unlike the session, the **Result Data** are stored **permanently** in the JATOS server, and will never be deleted automatically. So, store any information that might be useful for data analysis in the result data.

Unlike the **JSON Input Data** workers can write into the session through jatos.js. They can only read the JSON Input data. The JSON Input data is set by the experimenter in JATOS' GUI and typically used to configure the study. Another difference is that the JSON Input Data are exported/imported together with a study - but not the session.

### Comparative Overview

| | Batch Session     | Group Session     | Study Session     |
|-|-------------------|-------------------|-------------------|
| **Scope (accesible by)** | All workers in a batch | All workers in a group | All components in a study |
| **Usage** | Exchange and store data relevant for all members of a batch | Exchange and temporarily store data relevant for all members of a group | Exchange and temporarily store data between components of a single study run |
| **Example use** | (Pseudo-)randomly assign conditions to different workers; Combine results from different groups working in the same batch | Store choices of the two members of a Prisoner's Dilemma game | Pass on correct answers between components; Keep track of the number of iterations of a given component that is repeated |
| **Lifetime** | Survives after all workers finished their studies | Automatically deleted once the group is finished | Deleted once the worker finished the study - Hence temporary|
| **Updated when and via** | Any time you call one of the [jatos.batchSession funtions](jatos.js-Reference.html#functions-to-access-the-batch-session) | Any time you call one of the [jatos.groupSession funtions](jatos.js-Reference.html#functions-to-access-the-group-session) | At the end of each component or if you call [jatos.setStudySessionData](jatos.js-Reference.html#jatossetstudysessiondatasessiondata-complete) |
| **Visible and editable from JATOS' GUI** | ![yes](images/ok-24.ico) | ![no](images/x-24.ico) | ![no](images/x-24.ico) |
| **Requires WebSockets** | ![yes](images/ok-24.ico) | ![yes](images/ok-24.ico) | ![no](images/x-24.ico) |
| **Included in exported studies** | ![no](images/x-24.ico) | ![no](images/x-24.ico) | ![no](images/x-24.ico) |

### Example Study

We have an [example study](Example-Studies.html#study-group-and-batch-session-example-study), where we show the three different session types in action. Try it yourself:

1. Download and import the study. You'll find that the study contains two components: "First" and "Second". 

1. Run the study once: easiest is as a JATOS worker (just click 'Run' on the study bar, not on any of the component bars).

1. The first component will prompt you for a name. It will then write the name you enter here into the **Study Session**. Because all components have access to the Study Session, the second component can read it and use your name in a chat window.

   ![First component screenshot](images/ChatExample_1.png)

1. When you click on 'Next', the second component will load. Here you will see two chat windows: The left one is called the group chat because it uses the Group Session; the right one is called batch chat because it uses the Batch Session. For now you're alone in these chat rooms. So, without closing this run and from new browser tabs, **run the study 2 more times (at least)**. You can choose any worker type you want. Additional runs with the JATOS worker will work but you can also [use other worker types](Run-your-Study-with-Batch-Manager-and-Worker-Setup.html#worker-setup).

   ![Second component screenshot](images/ChatExample_2.png)

1. Now you have 3 simultaneous study runs. You will notice while writing into the group chat that two of your workers are in the same group - the third one has their own group. Why 2 per group? Because we [set the groups to a maximum of 2 members each](Group-Study-Properties.html#group-settings-in-each-batchs-properties). The group chat will use the **Group Session** to allow the 2 members of each group to communicate with each other. Members of other groups will not have access to the chats of this group. However, anything written into the **Batch Session** will be accesssible by all workers that are members of this batch, regardless of the group they're in.

   ![Second component screenshot](images/ChatExample_3.png)
   ![Second component screenshot](images/ChatExample_4.png)

