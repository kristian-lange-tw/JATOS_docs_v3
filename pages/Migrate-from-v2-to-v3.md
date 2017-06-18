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

Updating from JATOS 2 to JATOS 3 in either your local or server installation is mostly straightforward: most studies you wrote for JATOS 2 will work for JATOS 3 out of the box. (Although we added some nice new features like the batch session or the user manager). The only exception are studies that used the group session: you'll have to change a couple of functions to access the group session, and we suggest you consider whether the new batch session might [suit your needs](Session-Data-Three-Types.html#when-to-use) better than the group session. 

## Update your studies - changes in jatos.js

If you used the **group session**, you'll have to change a couple of lines in your JavaScript. Here's what changed: 
We abolished the direct access to the group session data with `jatos.groupSessionData`. Now you can only accesse it via several functions with the form:  `jatos.groupSession.[functionName]`, e.g. `jatos.groupSession.get()` and `jatos.groupSession.set()`. Find details in the [jatos.js Reference / Functions to access the group session](jatos.js-Reference.html#functions-to-access-the-group-session), or in [Write Your Own Group Studies](Write-Your-Own-Group-Studies.html), or in [Session Data - Three Types](Session-Data-Three-Types.html). 

Just a short example: To get your JATOS 2 code running in JATOS 3, simply change: 

* Writing to the group session: `jatos.groupSessionData = myObject;` -> `jatos.groupSession.setAll(myObject);`

* Reading from the group session: `var myObject = jatos.groupSessionData;` -> `jatos.groupSession.getAll();`

But consider going beyond this quick fix: the new group session offers much finer access with other functions, not just the setAll and getAll (which is why we changed them, not *just* to annoy you!). Additionally, we recommend to use the callback / promise functions in case something fails.

Also, consider that JATOS 3 includes the **batch session** and things (like [randomize conditions between participants](Example-Studies.html#randomize-conditions-between-participants-go---no-go-task)) that have you previously did with the group session can be now done easier with the batch session. Handling the batch session doesn't involve joining a group first - the batch channel is opened automatically by jatos.js for you.

## Update your local JATOS installation

Just follow [Update JATOS](Update-JATOS.html) - remember to stop JATOS and to make backups before doing anything.

## Update your server JATOS installation

Follow [Updating a JATOS server installation](Updating-a-JATOS-server-installation.html).

With JATOS 3 now requires (it's no longer optional) support for WebSockets (otherwise the batch and group session wouldn't work). So if you use a proxy in front of JATOS it has to be configured accordingly. You can find examples for [Apache](JATOS-with-Apache.html) and [Nginx](JATOS-with-Nginx.html) in this documentation.

## Keep your database with the update

The structure of the database changed from JATOS 2 to JATOS 3. Upgrading it is not difficult, but keep in mind that this is irreversible: while JATOS 3 can read result data exported from JATOS 2, the opposite direction won't work. So always back up your database in a safe place before upgrading, in case anything goes wrong.  


