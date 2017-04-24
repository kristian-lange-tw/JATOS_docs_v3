---
title: Two Types of Session Data
keywords: session data, Study Session, group session
tags:
summary:
sidebar: mydoc_sidebar
permalink: Two-Types-of-Session-Data.html
folder:
toc: false
last_updated: 28 Dec 2016
---

Often you want to store information during a study run and share it with other components of the same study, or - if it is a group study - within the group. For this JATOS provides the Session Data. There are two different Session Data types, both of which are stored **temporarily** in your database, and will be deleted once they are no longer in use.

The difference between session data and the result data is that the results are stored **permanently** in the database, and will stay there after the study is finished. All results should therefore go into the result data. 

### Study Session Data

The Study Session Data is useful to share information between components of a given study. Some examples include: 

* Sending information about percentage of correct responses in component 1 to component 2.
* Having a study-wide progress bar, showing how much of the entire study has been completed.
* Keeping track of the number of iterations of a given component that is repeated.

### Group Session Data

The Group Session Data is useful to share information between members of a given group. Some examples include:

* Responses to each trial in a group study like the Prisoner's Dilemma
* gender of group members 
