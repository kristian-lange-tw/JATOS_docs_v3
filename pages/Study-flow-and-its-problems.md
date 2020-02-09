---
title: Study Flow and its problems - reloading, linear studies, single-use workers and previews
keywords: preview, flow, study flow, linear study flow, allow reload, reloading, back, backwards, loop
tags:
summary:
sidebar: mydoc_sidebar
permalink: Study-flow-and-its-problems.html
folder:
toc: true
last_updated: 9 Feb 2020
---

## Study flow and it's problems

Let's first say what we understand under the _study flow_:

**Study flow** - the intended order of a study's componenents as they are done by the participants running the study. This doesn't necessarily has to be the order of components like they are defined in the study page, meaning going forward one-by-one - instead the study flow can go backwards to a previous component, go in a loop over several components, or reload the current component. It is even possible to decide on-the-fly in your study's JavaScript what the next component will be. In general and by default a component can go to any other component including itself. The _jatos.js_ functions to determine the study flow are `jatos.startNextComponent`, `jatos.startComponentByPos`, `jatos.startLastComponent` and `jatos.startComponent`.

**Common problems**
- You want to prevent a participant from reloading the same component (by using the browser's reload button).
- You want to ensure a linear study flow and prevent a study flow from going backbards (by using the browser's back button).
- You want to prevent a participant from running a study twice: If you are actually collecting data, you most likely want to ensure that each participant completes your study only once.
- You want to allow participants to first have a peek into a study and preview it without actually starting the study and fully commit to it.

... and their solutions:


## Allow reload or prevent a reload of the same component

A worker can press their browser's reload button and by default JATOS will respond with the same component again: the worker can do a component multiple times. To prevent this each component properties has a checkbox _Allow reload_.

![GUI Screenshot](images/component-properties-reload.png)

If you want to prevent this behaviour uncheck the box and then JATOS will respond with an error instead and the study run will be finished and put to state FAIL. Since each component properties has their own _Allow reload_ checkbox it can be defined differently for each component, e.g. reloading is allowed in the introduction but is prohibited in the actual experiment.

**Hint**: You should tell your workers in your study's description if you disallow reloads to prevent them from accidentally pressing the reload button and failing your study.

**Another hint**: The _Allow reload_ and the _Linear study flow_ properties can be combined to achieve a strictly increasing study flow.


## Ensure a linear study flow (since version 3.5.1)

A worker can press their browsers back button and by default JATOS will response with the previous component, the one that was done before by the worker. This might allow a worker to divert from the intended study flow. To prevent this each study properties has a checkbox _Linear study flow_.

![Study Properties Screenshot](images/study-properties-linear-flow.png)

If you want to enforce a linear study flow check the box. Then, if a worker tries to go backwards, JATOS will respond with an error instead and the study run will be finished and put to state FAIL.

**Hint**: You should tell your workers in your study's description if you enforce a linear study flow to prevent them from accidentally pressing the back button and failing your study.

**Another hint**: If you want to loop over components, un-check this box. 

**Yet another hint**: The _Allow reload_ and the _Linear study flow_ properties can be combined to achieve a strictly increasing study flow.


## Single-use worker links - prevent workers running the study twice

Often you want to prevent a worker from running the same study twice. To achieve this use the _single-use_ workers: that are the workers with 'Single' in their name, _Personal Single worker_ and _General Single worker_, and the _MTurk worker_.

Be aware that although _General Single_ links can be run only once from each browser and each computer, if the participant clears their browser's cookies, changes the browser or changes the computer, they will be able to run the study again.

[Read more on the different worker types available in JATOS](Worker-Types.html) 


### Preview Links

Then although you want to prevent running the same study twice you want to allow **General Single** or **Personal Single** workers to have a peek into the study, to preview it. The default behaviour is, once a worker clicked on the link - that's it, the study is started and JATOS will not allow a second click on this link. But in some cases you may want to distribute a link and let your workers preview the first component of your study (where you could e.g. describe what they will have to do, how long it will take, ask for consent, etc). Often, workers see this description and decide that they want to do the study later.

To allow them to do this, activate the checkbox **Allow preview** (this will add a `&pre` to the end of the URL).

![GUI Screenshot](images/preview_general_single_run.png)

Now your workers can use the link as often as they want - as long **as they don't go further than the first component**. But once the second component is started, JATOS will restrict access to the study in the usual way as it is for General Single and Personal Single workers. This means that they will get an error if they try to use the link again to access the study.
