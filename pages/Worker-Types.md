---
title: Worker Types
keywords: worker types, Jatos Worker, Personal Single Worker, Personal Multiple Worker, MTurk Worker, Preview Links
tags:
summary: Following Amazon Mechanical Turk’s terminology, a worker in JATOS is a person who runs a study. Different worker types access a study in different ways. For example, some workers can run the same study multiple times, whereas others can do it only once. 
sidebar: mydoc_sidebar
permalink: Worker-Types.html
folder:
toc: true
last_updated: 28 Dec 2016
---

### Overview

| | Jatos             | Personal Single   | Personal Multiple | MTurk             | General Single    | 
|-|-------------------|-------------------|-------------------|-------------------|-------------------|
| **Icon** | ![](images/jatos-24.png) | ![](images/personal_single-24.png) | ![](images/personal_multiple-24.png) | ![](images/mturk-24.png) | ![](images/general_single-24.png) |
| **Typical use** | During study development | Small targeted group, each one of them gets a link | Small targeted group of workers who pilot the study or need to do it multiple times | For Amazon Mechanical Turk | Bigger groups but with less control; link shared e.g. via social media |
| **Created when?** | Together with the JATOS user | By yourself in the Worker Setup | By yourself in the Worker Setup | On-the-fly after a MTurk worker clicked on the HIT link | On-the-fly whenever someone clicks on the link |
| **Run different studies with the same worker ID** | ![yes](images/ok-24.ico) | ![no](images/x-24.ico) | ![no](images/x-24.ico) | ![yes](images/ok-24.ico) | ![no](images/x-24.ico) |
| **Repeat the same study with the same worker ID** | ![yes](images/ok-24.ico) | ![no](images/x-24.ico) | ![yes](images/ok-24.ico) | ![no](images/x-24.ico) | ![no](images/x-24.ico) |
| **Supports [preview of studies](Worker-Types.html#preview-links)** | ![no](images/x-24.ico) | ![yes](images/ok-24.ico) | ![no](images/x-24.ico) | ![no](images/x-24.ico) | ![yes](images/ok-24.ico) |
| **Possible bulk creation** | ![no](images/x-24.ico) | ![yes](images/ok-24.ico) | ![yes](images/ok-24.ico) | ![no](images/x-24.ico) | ![no](images/x-24.ico) |
| **Run [group studies](Example-Group-Studies)** | ![yes](images/ok-24.ico) | ![yes](images/ok-24.ico) | ![yes](images/ok-24.ico) | ![yes](images/ok-24.ico) | ![yes](images/ok-24.ico) |


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

### Preview Links
A normal **General Single** or **Personal Single** is restrictive: once a worker clicked on the link - that's it. JATOS will not let them run the study twice. But in some cases you may want to distribute a link and let your workers preview the first component of your study (where you could e.g. describe what they will have to do, how long it will take, ask for consent, etc). Often, workers see this description and decide that they want to do the study later. To allow them to do this, activate the checkbox **Allow preview** (this will add a `&pre` to the end of the URL). Now your workers can use the link as often as they want - as long as they don't go further than the first component. But once the second component is started, JATOS will restrict access to the study in the usual way as it is for General Single and Personal Single workers. This means another usage of the link will lead to an error.

![GUI Screenshot](images/preview_general_single_run.png)
