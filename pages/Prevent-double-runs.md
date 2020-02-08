---
title: Prevent a participant from running a study twice
keywords: jatos.js, worker types, preview, linear study flow, prevent reload
tags:
summary:
sidebar: mydoc_sidebar
permalink: Prevent-double-runs.html
folder:
toc: true
last_updated: 8 Feb 2020
---

"Prevent repeated study runs": preview feature (from worker types), linear study flow, reload component, link to worker types (Eli)



If you are piloting or trying out the code for a study yoi will most likely use a Jatos Worker or a Personal Multiple 
or General Multiple Worker types. If you are actually collecting data, you most likely want to ensure that each participant 
completes your study only once. At the same time, you may want to let them 'sneak peek' the study before they commit to running it. 

You can use the following features to get this flexibilty

### Preview Links

A normal **General Single** or **Personal Single** link is restrictive: once a worker clicked on the link - that's it. JATOS will not let them run the study twice. But in some cases you may want to distribute a link and let your workers preview the first component of your study (where you could e.g. describe what they will have to do, how long it will take, ask for consent, etc). Often, workers see this description and decide that they want to do the study later.

To allow them to do this, activate the checkbox **Allow preview** (this will add a `&pre` to the end of the URL). Now your workers can use the link as often as they want - as long as they don't go further than the first component. But once the second component is started, JATOS will restrict access to the study in the usual way as it is for General Single and Personal Single workers. This means that you'll get an error if you try to use the link again to access the study.

![GUI Screenshot](images/preview_general_single_run.png)
