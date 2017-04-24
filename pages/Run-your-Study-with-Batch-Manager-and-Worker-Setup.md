---
title: Run your Study with Batch Manager & Worker Setup
keywords: batch manager, worker setup, worker, batch properties, worker setup, group properties
tags:
summary:
sidebar: mydoc_sidebar
permalink: Run-your-Study-with-Batch-Manager-and-Worker-Setup.html
folder:
toc: true
last_updated: 28 Dec 2016
---

If you run a study during development from within the JATOS GUI you will do so as a Jatos worker. There are [other worker types](Worker-Types.html) to distribute to real participants.

A worker in JATOS is a person who runs a study. A batch organizes workers and their study runs and results. Each study has a Batch Manager.

**Generate links to send to your workers**

For all worker types except Jatos and MTurk you'll need to generate links to send to your potential workers, which they can follow to access and run your study. Those links are generated in the **Worker Setup** (Batch Manager --> Worker Setup).

## Restrictions

1. Common to all worker types is that **the same worker can do only one study at the same time**. If a worker is running a study and starts another study run, the first study run will automatically be finished with an error. This is independent of whether the study runs are in the same or different browsers.

1. **[Valid only for versions 2.1.12 and older]**
**The same browser can only run one study at the same time**. If you start a second study in a browser where you have started a first study, the first study will automatically be finished with an error.

1. **[Valid only for versions 2.2.1 and newer]**
**The same browser can run one study in up to 10 different tabs**. This is useful if you want to test a group study. You can open up to 10 different tabs in the same browser (with a personal multiple link or as the jatos worker) and all these 10 "different" workers will interact with each other. Once you open the 11th tab, the first worker will be thrown out of the group. 

## Batch Manager

Since JATOS 2 you run studies in batches. A batch consists of its properties and a collection of workers that do the study. Using different batches is useful to organize your study runs, separate their results and vary their setup. E.g. you could separate a pilot run from the 'proper' experiment, or you could use different batches for different worker types.

Batches are organized in the Batch Manager. Here you can create and delete batches and access each batch's properties, worker setup and study results.

Each study comes with a 'Default' batch.

![Batch manager screenshot](images/batch manager.png)

### Batch Properties

For each batch, you can limit the maximum number of workers that will ever be able to run a study in this batch by setting the **Maximum Total Workers**.

![Batch manager screenshot](images/Batch Max worker types.png)

Additionally you can switch on or off worker types in the **Allowed Worker Types**. Forbidden worker types are not able to run a study. Always check before you send out links to study runs that the corresponding worker types are switched on. You can do the same in the Worker Setup.

![Worker types](images/Batch Max total workers.png)

The **Group Properties** relate to [group studies](Group-Study-Properties.html).

### Worker Setup

![Worker types](images/Worker types screenshot.png)

This is the place where you generate the links to study runs for most of your workers types (except for Jatos and MTurk). 

For **Personal Single Workers** and **Personal Multiple Workers** click **Add**. You can enter a worker description or identification in the 'Comments' box.

**General Single Workers** only have one link and each link will create a new separate worker. Get this link by clicking on **Link** in its row.

How to connect to MTurk and create links to run for **MTurk Workers** is described in the page [Connect to Mechanical Turk](Connect-to-Mechanical-Turk.html).

The differences between the worker types is explained in the [Worker Types page](Worker-Types.html).
