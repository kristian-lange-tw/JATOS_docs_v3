---
title: Worker Types
keywords: worker types, Jatos Worker, Personal Single Worker, Personal Multiple Worker, MTurk Worker, General Single Worker, General Multiple Worker, MTurk Sandbox Worker, MTurk, Sandbox, General, Single, Multiple, Personal, Preview Links
tags:
summary: Following Amazon Mechanical Turk’s terminology, a worker in JATOS is a person who runs a study. Different worker types access a study in different ways. For example, some workers can run the same study multiple times, whereas others can do it only once. 
sidebar: mydoc_sidebar
permalink: Worker-Types.html
folder:
toc: true
last_updated: 04 Sep 2018
---

### Overview

| | Jatos             | Personal Single   | Personal Multiple | General Single    | General Multiple (since v3.3.2)  | MTurk            |
|-|-------------------|-------------------|-------------------|-------------------|-------------------|------------------|
| **Icon** | <span class="glyphicon glyphicon-wrench glyphicon-jatos"></span> | <span class="glyphicon glyphicon-leaf glyphicon-personal-single"></span> | <span class="glyphicon glyphicon-tree-deciduous glyphicon-personal-multiple"></span> | <span class="glyphicon glyphicon-glass glyphicon-general-single"></span> | <span class="glyphicon glyphicon-asterisk glyphicon-general-multiple"></span> | <span class="glyphicon glyphicon-knight glyphicon-mturk"></span> |
| **Typical use** | During study development | Small targeted group, each one of them gets a link | Small targeted group of workers who pilot the study or need to do it multiple times | Bigger groups but with less control; link shared e.g. via social media | Bigger groups and where the workers need to do it multiple times | For Amazon Mechanical Turk |
| **Created when?** | Together with the JATOS user | By yourself in the Worker Setup | By yourself in the Worker Setup | On-the-fly whenever someone uses the link | On-the-fly whenever someone uses the link | On-the-fly after a MTurk worker clicked on the HIT link |
| **Run different studies with the same worker** | <span class="glyphicon glyphicon-ok-sign"></span> | <span class="glyphicon glyphicon-remove-sign"></span> | <span class="glyphicon glyphicon-remove-sign"></span> | <span class="glyphicon glyphicon-remove-sign"></span> | <span class="glyphicon glyphicon-remove-sign"></span> | <span class="glyphicon glyphicon-ok-sign"></span> |
| **Repeat the same study with the same link** | (has no links) | <span class="glyphicon glyphicon-remove-sign"></span> | <span class="glyphicon glyphicon-ok-sign"></span><br>(keeps the same worker) | <span class="glyphicon glyphicon-remove-sign"></span> | <span class="glyphicon glyphicon-ok-sign"></span><br>(creates a new worker each time) | <span class="glyphicon glyphicon-remove-sign"></span> |
| **Supports [preview of studies](Worker-Types.html#preview-links)** | <span class="glyphicon glyphicon-remove-sign"></span> | <span class="glyphicon glyphicon-ok-sign"></span> | <span class="glyphicon glyphicon-remove-sign"></span> | <span class="glyphicon glyphicon-ok-sign"></span> | <span class="glyphicon glyphicon-remove-sign"></span> | <span class="glyphicon glyphicon-remove-sign"></span> |
| **Possible bulk creation** | <span class="glyphicon glyphicon-remove-sign"></span> | <span class="glyphicon glyphicon-ok-sign"></span> | <span class="glyphicon glyphicon-ok-sign"></span> | <span class="glyphicon glyphicon-remove-sign"></span> | <span class="glyphicon glyphicon-remove-sign"></span> | <span class="glyphicon glyphicon-remove-sign"></span> |
| **Run [group studies](Example-Group-Studies)** | <span class="glyphicon glyphicon-ok-sign"></span> | <span class="glyphicon glyphicon-ok-sign"></span> | <span class="glyphicon glyphicon-ok-sign"></span> | <span class="glyphicon glyphicon-ok-sign"></span> | <span class="glyphicon glyphicon-ok-sign"></span> | <span class="glyphicon glyphicon-ok-sign"></span> |


### Jatos Worker
Jatos workers run a study (or any of its components individually) by clicking on the _Run_ buttons from the GUI. Jatos workers are usually the researchers trying out their own studies. Each JATOS user (i.e., anybody with a JATOS login) has their own Jatos worker.  
**Jatos workers can run the same study as many times as they want.**

### Personal Single Worker 
These are external workers that can **only run the study once** ([*But see Preview Links](#preview-links)).
You send a _Personal Single_ link to workers that you contact individually. Each link can be personalized with a **Comment** you provide while creating it (e.g. by providing a pseudonym). 
Personalized single links with single access are useful in small studies, where it's feasible to contact each worker individually, or (e.g.) you want to be able to pair up several results (either from the same or different studies) in a longitudinal design. You can add in bulk up to 100 Personal Single Workers at once by changing the **Amount** value.

![GUI Screenshot](images/create_personal_single_run.png)
![GUI Screenshot](images/view_personal_single_run.png)

### Personal Multiple Worker (personal with multiple access)
These are external workers that **can run a study as many times as they want**. You could send _Personal Multiple_ links to your pilot workers. Each link can be personalized with a **Comment** you provide while creating it (e.g. by providing a pseudonym). You can add in bulk up to 100 Personal Multiple Workers at once by changing the **Amount** value.

### MTurk Worker
MTurk workers access a study **only once**, through a link in Amazon's Mechanical Turk (AMT). Each MTurk worker in JATOS corresponds to a single worker in AMT. 

**DATA PRIVACY NOTE:** If the same worker from AMT does two of your studies, the two results will be paired with the same MTurk Worker in JATOS. This means that you could gather data from different studies, without your workers ever consenting to it. For this reason, we recommend that you delete your data from JATOS as soon as you finish a study. This way, if the same worker from AMT takes part in a different study, they will get a new MTurk Worker, and you will not be able to automatically link their data between different studies. See our [Data Privacy and Ethics](Data-Privacy-and-Ethics) page for more details on this.  

### General Single Worker 
These are external workers that can **run a study only once** ([*But see Preview Links](#preview-links)). You could distribute a _General Single_ link through a mailing list or posting it on a public website. It is essentially useful for cases where you want to collect data from a large numbers of workers. Each new worker accessing the study will be assigned a new General Single Worker. 

Keep in mind, however, that JATOS uses the browser's cookies to decide whether a worker has already accessed a study. If a worker uses a different computer, a new browser, or simply deletes their browser's cookies, then JATOS will assume that it's a new worker. So the same person can easily use a General Single link several times.  

### General Multiple Worker (since version 3.3.2)
A General Multiple link can be used many times by different participants and even by the same participant using the same browser - this link type is the least restrivtive one. Each time it is used a new General Multiple Worker is created on-the-fly.



### Preview Links
A normal **General Single** or **Personal Single** is restrictive: once a worker clicked on the link - that's it. JATOS will not let them run the study twice. But in some cases you may want to distribute a link and let your workers preview the first component of your study (where you could e.g. describe what they will have to do, how long it will take, ask for consent, etc). Often, workers see this description and decide that they want to do the study later. To allow them to do this, activate the checkbox **Allow preview** (this will add a `&pre` to the end of the URL). Now your workers can use the link as often as they want - as long as they don't go further than the first component. But once the second component is started, JATOS will restrict access to the study in the usual way as it is for General Single and Personal Single workers. This means another usage of the link will lead to an error.

![GUI Screenshot](images/preview_general_single_run.png)
