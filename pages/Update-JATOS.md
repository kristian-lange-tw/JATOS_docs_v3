---
title: Update JATOS
keywords: update
tags:
summary:
sidebar: mydoc_sidebar
permalink: Update-JATOS.html
folder:
toc: true
last_updated: 29 Dec 2016
---

We'll periodically update JATOS with new features and bug fixes. We recommend you stay up to date with the [latest release](https://github.com/JATOS/JATOS/releases). However if you are currently running a study it's always safest to keep the same JATOS version throughout the whole experiment.

## Updating a local installation of JATOS 
(The procedure is different if you want to [update JATOS on a server installation](Updating-a-JATOS-server-installation.html))

To be absolutely safe you can install the new JATOS version and keep the old one untouched. This way you can switch back if something fails. Just remember that only one JATOS can run at the same time. Always end JATOS before starting another one.

You can update your local JATOS instance in two main ways:
 
### First, easy way: discarding your result data

If you don't care about result data stored in JATOS:

1. Export any studies you wish to keep from the old JATOS installation.
1. Download and install the new version as if it were a new fresh download. Don't start it yet.
1. Stop the old JATOS and start the new JATOS.
1. Import all the studies your previously exported. This will transfer the files and subfolders in your study's asset folder (HTML, JavaScript, CSS files). 

**What will be transferred:**

1. Files and subfolders in study's assets folder
1. All your studies' and components' properties
1. The **properties** of the first (Default) batch
 
**What will be lost:** 

1. **All result data will be lost**
1. All workers in all batches (including Default batch)
1. All batches other than the Default batch

### Second way: keeping everything (including your result data)

If you do want to keep your studies, batches, and your result data you'll have to move them to the new JATOS. 

**However: Occasionally (on major version updates such as 1.X.X to 2.1.1) we will make big changes in JATOS, which will require some restructuring of the database. In these cases, the second way described here will not be possible. We will do our best to prevent these big changes and inform you explicitly in the release description.**

1. Stop JATOS (on Unix systems, type `$ ./loader.sh stop` on the terminal. On Windows MS, close your command window)
1. Go to the folder of your old JATOS installation. From there copy your assets root folder to the new JATOS installation (Note: By default your assets root folder is called `study_assets_root` and lays in the JATOS folder but you might have changed this. You can find the location and name in `conf/production.conf`. It is specified in the line beginning with `jatos.studyAssetsRootPath=`.)
1. From your the folder of your old JATOS installation copy the folder `database` to the new JATOS installation.
1. If you had changed the `conf/production.conf` file in your old JATOS instance (for example to set a custom location for your `study_assets_root` folder) you'll have to do this again in the new JATOS version. We recommend re-editing the new version of the file, rather than just overwriting the new with the old version, in case anything in the `production.conf` file has changed.
1. That's it! Start the new JATOS.

**What will be transferred:**

1. Files and subfolders in study assets folder
1. All your study and components properties
1. All batches, together with their workers, generated links, and results

**What will be lost:**
nothing
