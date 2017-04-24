---
title: Updating a JATOS server installation
keywords: update, server
tags:
summary:
sidebar: mydoc_sidebar
permalink: Updating-a-JATOS-server-installation.html
folder:
toc: true
last_updated: 29 Dec 2016
---

Updating the server instance is equivalent to doing it [locally](Update-JATOS.html), but make sure that you know what you're doing; especially if you have paired JATOS with a MySQL database.

To be absolutely safe you can install the new JATOS version and keep the old one untouched. This way you can switch back if something fails. Just remember that only one JATOS can run at the same time.

Note: If you are using a MySQL database and to be on the safe side in case something goes wrong, make a backup of your MySQL database. Dump the database using `mysqldump -u yourUserName -p yourDatabaseName > yourDatabaseName.out`.

As when [updating of a local JATOS installation](Update-JATOS.html) you have two options: 1. Keep your studies but discard all your result data and batches. 2. Keep everything, including your studies and result data (might not always be possible).

### First option: quick and dirty (discarding result data)

You can just follow the [update instructions for the local installation](Update-JATOS.html#first-easy-way-discarding-your-result-data). If you use a mySQL database don't forget to [configure it with a clean and new one](Configure-JATOS-on-a-Server.html) (not the one from your old JATOS). Do not use the new JATOS with the old MySQL database unless you choose to keep your data, as described below.

### Second option: keeping everything

This means that we have to configure the MySQL database or copy the H2 database files.

**However: Occasionally (on major version updates such as 1.X.X to 2.1.1) we will make big changes in JATOS, which will require some restructuring of the database. In these cases, the second way described here will not be possible. We will do our best to prevent these big changes and inform you explicitly in the release description.**

1. Stop the old JATOS using `./loader.sh stop` 
1. Copy the new JATOS version to your server, e.g. copy it into the same folder where your old JATOS is located. Don't yet remove the old JATOS instance. 
1. Unzip the new JATOS (`unzip jatos-x.x.x-beta.zip`)
1. From the old JATOS installation copy your assets root folder to the new JATOS installation (Note: By default your assets root folder is called `study_assets_root` and lays in the JATOS folder but you might have [changed this](Configure-JATOS-on-a-Server.html).
1. If you are using the default H2 database: From your the folder of your old JATOS installation copy the folder `database` to the new JATOS installation. For an external MySQL or H2 database you don't have to change anything on the database side.
1. [Configure the new JATOS like the old one](Configure-JATOS-on-a-Server.html)
1. That's it! Start the new JATOS using `./loader.sh start`
 
