---
title: Prevent a participant from running a study twice
keywords: jatos.js, worker types, preview, linear study flow, allow reload
tags:
summary:
sidebar: mydoc_sidebar
permalink: Prevent-double-runs.html
folder:
toc: true
last_updated: 8 Feb 2020
---

If you are piloting or trying out the code for a study yoi will most likely use a Jatos Worker or a Personal Multiple 
or General Multiple Worker types. If you are actually collecting data, you most likely want to ensure that each participant 
completes your study only once. At the same time, you may want to let them 'sneak peek' the study before they commit to running it. 

You can combine the following features to get this flexibilty

### Single-use worker links

* Personal Single links are the safest: once a study has been started with that link, it cannot be started again. 
* MTurk worker links are also safe in that each MTurk Worker ID can click on the link only once.  
* General Single links can be run once from each browser and each computer. If the same person clears heir cookies, changes browser, or changes computer, they will be able to run the study again. 
[Read more](Worker-Types.html) on the different worker types available 


### Preview Links (keep here or keep in worker links or keep in both?)

A normal **General Single** or **Personal Single** link is restrictive: once a worker clicked on the link - that's it. JATOS will not let them run the study twice. But in some cases you may want to distribute a link and let your workers preview the first component of your study (where you could e.g. describe what they will have to do, how long it will take, ask for consent, etc). Often, workers see this description and decide that they want to do the study later.

To allow them to do this, activate the checkbox **Allow preview** (this will add a `&pre` to the end of the URL). Now your workers can use the link as often as they want - as long as they don't go further than the first component. But once the second component is started, JATOS will restrict access to the study in the usual way as it is for General Single and Personal Single workers. This means that you'll get an error if you try to use the link again to access the study.

![GUI Screenshot](images/preview_general_single_run.png)

### Allow Reload option in each component

Apart from not allowing a participant to use a link twice, you might want to prevent participants from reloading the experimental script in their browser. This is the case by default: if participants reload a page, this message appears: "A problem occurred:
It's not allowed to reload this component (component ID). Study (study ID) is finished.". And the State of the Study Run is set to FAIL in your result data. You can override this option by checking the box "Allow reload" in each individual component's properties window. This is useful if you are trying out a study (or if you want to loop over components?)

### Linear study flow

If you have a study with more than one component, you might want to *also* prevent participants from navigating backwards in their browser, and re-starting an earlier component. To do this, check the box 'Linear study flow' in the Study Properties. If a participant tries to navigate backwards, they will get this message: "A problem occurred: Study [study name] (Study ID) allows only linear study flow. But component (component ID) attempted to start component (previous component ID). The study is finished." And the Stutus of the study result is also set to FAIL. If you want to loop over components, un-check this box.    

![Study Properties Screenshot](images/linearStudyFlow.png)
