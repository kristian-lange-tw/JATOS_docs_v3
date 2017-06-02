---
title: Session Data - Three Types
keywords: session data, Study Session, group session, batch session
tags:
summary:
sidebar: mydoc_sidebar
permalink: Session-Data-Three-Types.html
folder:
toc: false
last_updated: 2 June 2017
---

Often you want to store information during a study run and share it with other components of the same study, or between workers of a group or batch. For this purpose, use one of the three different Session Data types available.

Unlike the session data, the **Result Data** are stored **permanently** in the JATOS server, and will never be deleted automatically. So, store any information that might be useful for data analysis in the result data.

Unlike the **JSON Input Data** workers can write into the session data through jatos.js. They can only read the JSON input data. The JSON input data is set by the experimenter in JATOS' GUI and typically used to configure the study. Another difference is that the JSON Input Data are exported/imported together with a study - but not the session data.

### Comparative Overview

| | Batch session     | Group Session     | Study Session     |
|-|-------------------|-------------------|-------------------|
| **Scope (accesible by)** | All workers in a batch | All workers in a group | All components in a study |
| **Usage** | Exchange and store data relevant for all members of a batch | Exchange and temporarily store data relevant for all members of a group | Exchange and temporarily store data between components of a single study run |
| **Example use** | (Pseudo-)randomly assign conditions to different workers; Combine results from different groups working in the same batch | Store choices of the two members of a Prisoner's Dilemma game | Pass on correct answers between components; Keep track of the number of iterations of a given component that is repeated |
| **Lifetime** | Survives after all workers finished their studies | Automatically deleted once the group is finished | Deleted once the worker finished the study - Hence temporary|
| **Updated when and via** | Any time you call one of the [jatos.batchSession funtions](jatos.js-Reference.html#functions-to-access-the-batch-session) | Any time you call one of the [jatos.groupSession funtions](jatos.js-Reference.html#functions-to-access-the-group-session) | At the end of each component or if you call [jatos.setStudySessionData](jatos.js-Reference.html#jatossetstudysessiondatasessiondata-complete) |
| **Visible and editable from JATOS' GUI** | ![yes](images/ok-24.ico) | ![no](images/x-24.ico) | ![no](images/x-24.ico) |
| **Requires WebSockets** | ![yes](images/ok-24.ico) | ![yes](images/ok-24.ico) | ![no](images/x-24.ico) |
| **Included in exported studies** | ![no](images/x-24.ico) | ![no](images/x-24.ico) | ![no](images/x-24.ico) |

### Example implementation

In the example study [study__group__and_batch_session](Example-Studies.html#study__group__and_batch_session), we show the three different session data in action. To see how it works, we suggest:

1. Download and import the study. You'll find that the study contains two components: "First" and "Second". 
1. Run the study once as a JATOS user (just click 'Run' on the study bar, not on any of the component bars).
1. The first component will prompt you for your name, and then write the name you enter here into the **Study session data**. Because all components have access to the Study session data, the second component will then read the session data and use your name in a chat window. 
1. When you click on 'Next', the second component will load. Here you will see two chat windows. The left one is called the Group chat because it uses the Group session data; the right one is called Batch chat because it uses the Batch session data. For now you're alone in these chat rooms. So, without closing this run and from a new browser tab, run the study **2 more times (at least)**. You can choose any worker type you want. Additional runs with the JATOS worker will work but you can also [get links](Run-your-Study-with-Batch-Manager-and-Worker-Setup.html#worker-setup) to other worker types.
1. Once you have (at least) 3 simultaneous workers, you'll see all features of this study. Why 3? Because we set the groups to a maximum of 2 members each. The group chat will use the **Group session data** to allow the 2 members of each group to communicate with each other. Members of other groups will not have access to the chats of this group. However, anything written into the **Batch session data** will be accesssible by all workers that are members of the batch, regardless of the group they're in.
1. To actually test the study, alternate between the open study runs (aka the open browser tabs running the study) to write into the group and session chat boxes. Note that the group chat is limited to the same group members, but the session chat is not.  


