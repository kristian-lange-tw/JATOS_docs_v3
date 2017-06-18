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

Updating from JATOS 2 to JATOS 3 in either your local or server installation is mostly straightforward: most studies you wrote for JATOS 2 will work for JATOS 3 out of the box. (Although we added some nice new features like the Batch Session or the user manager). The only exception are studies that used the Group Session: you'll have to change a couple of functions to access the Group Session.

## Update your studies - changes in jatos.js

If you used the **Group Session**, you'll have to change a couple of lines in your JavaScript. To get your JATOS 2 code running in JATOS 3, simply change: 

* Writing to the Group Session: `jatos.groupSessionData = myObject;` -> `jatos.groupSession.setAll(myObject);`

* Reading from the Group Session: `var myObject = jatos.groupSessionData;` -> `jatos.groupSession.getAll();`

But consider going beyond this quick fix: the new Group Session offers much finer access with other functions, not just the `setAll` and `getAll` (which is why we changed them, not *just* to annoy you!). Additionally, we recommend to use the callback / promise functions in case something fails.

To improve the Group Session, we abolished the direct access to the Group Session data with `jatos.groupSessionData`. Now you can only access it via several functions with the form: `jatos.groupSession.[functionName]`, e.g. `jatos.groupSession.get()` and `jatos.groupSession.set()`. Find details about the jatos.js functions to access the Group Session in the [jatos.js Reference / Functions to access the Group Session](jatos.js-Reference.html#functions-to-access-the-group-session) and examples of how to use them in [Write Your Own Group Studies](Write-Your-Own-Group-Studies.html). 

Also, consider that JATOS 3 includes the **Batch Session** and things (like [randomize conditions between participants](Example-Studies.html#randomize-conditions-between-participants-go---no-go-task)) that you previously did with the Group Session can now be done easier with the Batch Session. Handling the Batch Session doesn't involve joining a group first - the batch channel is opened automatically by jatos.js for you. Check out the differences between the group- and Batch Sessions in [Session Data - Three Types](Session-Data-Three-Types.html) to decide which session type is best for your needs. 

## Update your local JATOS installation

Just follow [Update JATOS](Update-JATOS.html) - remember to stop JATOS and to make backups before doing anything.

## Update your server JATOS installation

Follow [Updating a JATOS server installation](Updating-a-JATOS-server-installation.html).

With JATOS 3 now requires (it's no longer optional) support for WebSockets (otherwise the Batch and Group Session wouldn't work). So if you use a proxy in front of JATOS it has to be configured accordingly. You can find examples for [Apache](JATOS-with-Apache.html) and [Nginx](JATOS-with-Nginx.html) in this documentation.

## Keep your database with the update

The schema of the database changed from JATOS 2 to JATOS 3. JATOS does this automatically. But keep in mind that this is irreversible: once JATOS updated the database it can't be used in JATOS 2 anymore. So always back up your database in a safe place before upgrading, in case anything goes wrong.


