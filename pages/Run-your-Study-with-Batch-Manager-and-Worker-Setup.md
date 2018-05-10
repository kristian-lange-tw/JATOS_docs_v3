---
title: Run your Study with Worker & Batch Manager
keywords: batch manager, Worker and Batch Manager, Worker & Batch Manager, worker manager, worker setup, worker, batch properties, worker setup, group properties
tags:
summary:
sidebar: mydoc_sidebar
permalink: Run-your-Study-with-Batch-Manager-and-Worker-Setup.html
folder:
toc: true
last_updated: 9 May 2018
---

If you run a study during development from within the JATOS GUI you will do so as a Jatos worker. There are [other worker types](Worker-Types.html) to distribute to real participants.

A worker in JATOS is a person who runs a study. A batch organizes workers and their study runs and results. Each study has a Worker & Batch Manager.

**Generate links to send to your workers**

For all worker types except Jatos and MTurk you'll need to generate links to send to your potential workers, which they can follow to access and run your study. Those links are generated in the **Worker Setup** (Worker & Batch Manager --> Worker Setup).

**In the same browser one can run studies in up to 10 different tabs**

If more than 10 studies run in the same browser in parallel the oldest study is finished automatically. Of course this limitation doesn't apply with different browsers. One could ask why it's necessary to run several studies at once in the same browser - usually a worker should run only one?! This is actually very useful for developing and testing group studies or studies that use the Batch Session. You can open up to 10 different tabs in the same browser (with a personal multiple link or as the jatos worker) and all these 10 "different" workers will interact with each other. Once you open the 11th tab, the first worker will be thrown out of the group. 

## Worker & Batch Manager

**A batch is mostly a collection of workers together with some properties**

Since JATOS 2 you run studies in batches. A batch consists of its properties and a collection of workers that do the study. Using different batches is useful to organize your study runs, separate their results and vary their setup. E.g. you could separate a pilot run from the 'proper' experiment, or you could use different batches for different worker types.

Batches are organized in the Worker & Batch Manager. Here you can create and delete batches and access each batch's properties, worker setup and study results.

Each study comes with a 'Default' batch.

![Worker & Batch manager screenshot](images/batch_manager.png)

### Batch Properties

For each batch, you can limit the maximum number of workers that will ever be able to run a study in this batch by setting the **Maximum Total Workers**.

![Worker & Batch manager screenshot](images/batch_properties.png)

Additionally you can switch on or off worker types in the **Allowed Worker Types**. Forbidden worker types are not able to run a study. Always check before you send out links to study runs that the corresponding worker types are switched on. You can do the same in the Worker Setup.

The **Group Properties** relate to [group studies](Group-Study-Properties.html).

### Worker Setup

![Worker types](images/worker_setup.png)

This is the place where you generate the links to study runs for most of your workers types (except for Jatos and MTurk). 

For **Personal Single Workers** and **Personal Multiple Workers** click **Add**. You can enter a worker description or identification in the 'Comments' box.

**General Single Workers** only have one link and each link will create a new separate worker. Get this link by clicking on **Link** in its row.

How to connect to MTurk and create links to run for **MTurk Workers** is described in the page [Connect to Mechanical Turk](Connect-to-Mechanical-Turk.html).

The differences between the worker types is explained in the [Worker Types page](Worker-Types.html).
