---
title: JATOS Requirements
keywords: requiremtents, server, installation, install, MySQL, database, disk, memory, CPU
tags:
summary: 
sidebar: mydoc_sidebar
permalink: JATOS-requirments.html
folder:
toc: true
last_updated: 6 Aug 2020
---

If you have further questions about JATOS installation and its requirements, please [contact us](Contact-us.html). 

**Disk size** is mostly determined by the experiments the users are running on this JATOS server and is difficult to predict. In general, if an experiment uses or produces video, audio, or large image files the disk size can get very high. On the contrary, if an experiment just produces result data in text format, disk size tends to be low.

**Memory**: Absolute minimum is 1GB - anything else depends on your users and more importantly, how many experiments your users intend to run in parallel. Feasible numbers are 1GB, 2GB, 4GB or 8GB.

**CPU**: usually not the limiting factor - unless your users run many experiments in parallel

### Database

Although JATOS can run with its embedded database for a 'professional' setup a MySQL database is recommended. It can be on the same machine as JATOS is running or an extra machine. It is not necessary to set up tables etc - except for a user and the database itself all setup is done by JATOS automatically.

The database size, like the disk size, depends mostly on the experiments the users are running on the JATOS instance. Importantly, large files (video, audio, images) are usually stored in the file system and not in the database. That makes the database size requirements more predictable.

### Backup

Best is to tell your JATOS users to 'export' their result data regularly themselves - the less they will ask you.

A full JATOS backup consists of three directories in the file system and a MySQL dump. It can be done while JATOS is running (only if MySQL is used - not with the embedded database).

### Three Examples

#### Small group

A small research group intends to run reasonably sized experiments. The experiments do not involve uploading of large file. They expect a couple of hundreds or even thousands of participants per experiment. 

* memory: 2 to 4 GB memory
* disk: 40 - 100 GB
* CPU: yes

#### Institute installation

An institute with around 100 researchers. It's difficult to predict what size the experiments will be. Participant recruitment might happen via social networks and it is to be expected that many experiments will be started at the same time.

* memory: 8 GB
* disk: 100 GB - x TB (reasonable numbers are 1, 2, 4)
* CPU: 4