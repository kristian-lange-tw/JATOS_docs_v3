---
title: Migrate from JATOS 2 to JATOS 3
keywords: migration, update, upgrade, version, JATOS 2
tags: 
summary:
sidebar: mydoc_sidebar
permalink: Migrate-from-v2-to-v3.html
toc: false
last_updated: 18 June 2017
---

Although JATOS 3 has some nice new features (like the batch session or the user manager) there is not much to do when it comes to update your local or your server JATOS installation. Your studies should work on JATOS 3 if they worked on JATOS 2 - unless you used the group session. The access to the group session changed together with the introduction of the batch session. 

## Update your studies - changes in jatos.js

Like mentioned the access to the **group session** changed quite a bit. We abolished the direct access to the group session data with `jatos.groupSessionData`. Now it can be accessed via several functions:  `jatos.groupSession.[functionName]`, e.g. `jatos.groupSession.get()` and `jatos.groupSession.set()`. More information can be found directly under the [jatos.js Reference / Functions to access the group session](jatos.js-Reference.html#functions-to-access-the-group-session), or in [Write Your Own Group Studies](Write-Your-Own-Group-Studies.html), or in [Session Data - Three Types](Session-Data-Three-Types.html). 

Just a short example: Here is what you could do to make you JATOS 2 code run in JATOS 3 again. Although be aware that the group session offers much finer access with other functions. Additionally it's recommended to use the callback / promise functions in case something fails.

* Writing: `jatos.groupSessionData = myObject;` -> `jatos.groupSession.setAll(myObject);`

* Reading: `var myObject = jatos.groupSessionData;` -> `jatos.groupSession.getAll();`

Another point to consider is that with JATOS 3 comes the **batch session** and things (like [randomize conditions between participants](Example-Studies.html#randomize-conditions-between-participants-go---no-go-task)) that have been done with the group session can be done easier with the batch session now. Handling the batch session doesn't involve joining a group first - the batch channel is opened automatically by jatos.js for you.

## Update your local JATOS installation

Just follow [Update JATOS](Update-JATOS.html) - remember to stop JATOS and to make backups before doing anything.

## Update your server JATOS installation

Follow [Updating a JATOS server installation](Updating-a-JATOS-server-installation.html).

With JATOS 3 now it is mandatory to support **WebSockets** (otherwise the batch and group session wouldn't work). So if you use a proxy in front of JATOS it has to be configured accordingly. You can find examples for [Apache](JATOS-with-Apache.html) and [Nginx](JATOS-with-Nginx.html) in this documentation.

