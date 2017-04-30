---
title: Session Data - Three Types
keywords: session data, Study Session, group session, batch session
tags:
summary:
sidebar: mydoc_sidebar
permalink: Session-Data-Three-Types.html
folder:
toc: false
last_updated: 27 April 2017
---

Often you want to store information during a study run and share it with other components of the same study, or between workers of a group or batch. For this purpose, use one of the three different Session Data types available.

Unlike the session data, the **Result Data** are stored **permanently** in the JATOS server, and will never be deleted automatically. So, store any information that might be useful for data analysis in the result data.

Unlike the **JSON Input Data** workers can write into the session data through jatos.js. They can only read the JSON input data. The JSON input data is set by the experimenter in JATOS' GUI and typically used to configure the study.

### Comparative Overview

| | Batch session     | Group Session     | Study Session     |
|-|-------------------|-------------------|-------------------|
| **Scope (accesible by)** | All workers in a batch | All workers in a group | All components in a study |
| **Usage** | Exchange and store data relevant for all members of a batch | Exchange and temporarily store data relevant for all members of a group | Exchange and temporarily store data between components of a single study run |
| **Example use** | (Pseudo-)randomly assign conditions to different workers; Combine results from different groups working in the same batch | Store choices of the two members of a Prisoner's Dilemma game | Pass on correct answers between components; Keep track of the number of iterations of a given component that is repeated |
| **Lifetime** | Survives after all workers finished their studies | Automatically deleted once the group is finished | Deleted once the worker finished the study - Hence temporary|
| **Updated when and via** | Any time you call one of the [jatos.batchSession funtions](jatos.js-Reference.html#functions-to-access-the-batch-session) | Any time you call one of the [jatos.groupSession funtions](jatos.js-Reference.html#functions-to-access-the-group-session) | At the end of each component or if you call [jatos.setStudySessionData](jatos.js-Reference.html#jatossetstudysessiondatasessiondata-complete) |
| **Visible from JATOS' GUI** | ![yes](images/ok-24.ico) | ![no](images/x-24.ico) | ![no](images/x-24.ico) |
| **Requires WebSockets** | ![yes](images/ok-24.ico) | ![yes](images/ok-24.ico) | ![no](images/x-24.ico) |

