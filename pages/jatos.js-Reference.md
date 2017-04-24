---
title: jatos.js Reference
keywords: reference, jatos.js
tags:
summary: jatos.js is a small JavaScript library that helps you to communicate from JavaScript with your JATOS server (in more technical terms, it wraps calls to JATOS' public REST API). Below we list and describe the variables and functions of the jatos.js library.
sidebar: mydoc_sidebar
permalink: jatos.js-Reference.html
folder:
toc: true
last_updated: 28 Dec 2016
---

Two [bits of code](Mandatory-lines-in-your-components-HTML.html) are mandatory in all your components' HTML files. One of them is the following line in the head section: `<script src="/assets/javascripts/jatos.js"></script>` which includes the jatos.js library into your HTML file. 

All variables or calls to jatos.js start with `jatos.`. For example, if you want to get the study's ID you can use `jatos.studyId`. If you want to submit some result data of your component back to your JATOS server you can call `jatos.submitResultData(resultData)`, where resultData can be any kind text.

And, please, if you find a mistake or have a question don't hesitate to [contact us](Contact-us.html).

Below we list and describe the variables and functions of the jatos.js library:



## jatos.js variables

### IDs

You can call any of these variables below at any point in your HTML file after `jatos.onload()` is done. All those IDs are generated and stored by JATOS. jatos.js automatically sets these variables with the corresponding values if you included the `jatos.onLoad()` callback function at the beginning of your JavaScript.

* `jatos.studyId` - ID of the study which is currently running. All the study properties are associated with this ID.
* `jatos.componentId` - ID of the component which is currently running. All the component properties are associated with this ID.
* `jatos.batchId` - ID of the batch this study run belongs to. All batch properties are associated with this ID.
* `jatos.workerId` - Each worker who is running a study has an ID.
* `jatos.studyResultId` - This ID is individual for every study run. A study result contains data belonging to the run in general (e.g. study session).
* `jatos.componentResultId` - This ID is individual for every component in a study run. A component result contains data of the run belonging to the specific component (e.g. result data).

There's a convenient function that adds all these IDs to a given object. See function `jatos.addJatosIds(obj)` below.


### Study variables

* `jatos.studyProperties` - All the properties (except the JSON input data) you entered for this study
  * `jatos.studyProperties.title` - Study's title
  * `jatos.studyProperties.uuid` - Study's UUID
  * `jatos.studyProperties.description` - Study's description
  * `jatos.studyProperties.locked` - Whether the study is locked or not
  * `jatos.studyProperties.dirName` - Study's dir name in the file system of your JATOS installation
  * `jatos.studyProperties.groupStudy` - Whether this is a group study or not
* `jatos.studyJsonInput` - The JSON input you entered in the study's properties.
* `jatos.studyLength` - Number of component this study has


### Component variables

* `jatos.componentProperties` - All the properties (except the JSON input data) you entered for this component
  * `jatos.componentProperties.title` - Component's title
  * `jatos.componentProperties.uuid` - Component's UUID
  * `jatos.componentProperties.htmlFilePath` - Path to Component's HTML file in your JATOS installation
  * `jatos.componentProperties.reloadable` - Whether it's reloadable
* `jatos.componentJsonInput` - The JSON input you entered in the component's properties.
* `jatos.componentList` -  An array of all components of this study with basic information about each component. For each component it has the `title`, `id`, whether it is `active`, and whether it is `reloadable`.
* `jatos.componentPos` - Position of this component within the study starting with 1 (like shown in the GUI)


### Study's session data

The session data can be accessed and modified by every component of a study. It's a very convenient way to share data between different components. Whatever is written in this variable will be available in the subsequent components. However, remember that the session data will be deleted after the study is finished (see also [Two Types of Session Data](Two-Types-of-Session-Data.html)).

* `jatos.studySessionData`


### Batch variables

* `jatos.batchProperties` - All the properties you entered for this batch.
  * `jatos.batchProperties.allowedWorkerTypes` - List of worker types that are currently allowed to run in this batch.
  * `jatos.batchProperties.maxActiveMembers` - How many members this group can have at the same time
  * `jatos.batchProperties.maxTotalMembers` - How many members this group is allowed to have at the same time
  * `jatos.batchProperties.maxTotalWorkers` - Total amount of workers this group is allowed to have altogether in this batch
  * `jatos.batchProperties.title` - Title of this batch


### Group variables

The group variables are part of jatos.js since JATOS 2. They are only filled with values if the current study is a group study.

* `jatos.groupMemberId` - Group member ID is unique for this member (it is actually identical with the study result ID)
* `jatos.groupResultId` - ID of this group result (It's called group result to be consistent with the study result and the component result - although often it's just called group)
* `jatos.groupState` - Represents the state of the group in JATOS; only set if group channel is open (one of STARTED, FIXED, FINISHED)
* `jatos.groupMembers` - List of member IDs of the current members of the group
* `jatos.groupChannels` - List of member IDs of the currently open group channels


### Group's session data

* `jatos.groupSessionData` - Group session data shared in between members of the group (see also [Two Types of Session Data](Two-Types-of-Session-Data.html))


### Other variables

* `jatos.version` - Current version of the jatos.js library



## General jatos.js functions

### `jatos.onLoad(callback)`

Defines callback function that jatos.js will call when it's finished initialising. Only [mandatory](Mandatory-lines-in-your-components-HTML.html) call in every component.

### `jatos.onError(callback)`

Defines callback function that is to be called in case jatos.js produces an error.

### `jatos.log(logMsg)`

Logs an msg in the log of the JATOS installation.

* _param {String} logMsg_ - The messages to be logged

### `jatos.addJatosIds(obj)`

Convenience function that adds some [IDs](jatos.js-Reference.html#ids) (study ID, study title, component ID, component position, component title, worker ID, study result ID, component result ID, group result ID, group member ID) to the given object.

* _param {Object} obj_ - Object to which the IDs will be added

### `jatos.setHeartbeatPeriod(heartbeatPeriod)`

Every running component sends regularly a HTTP request (the heartbeat) back to the JATOS server. This signals that it is still running. As soon as the browser tab running the component is closed the heartbeat ceases. The time of the last heartbeat is visible in the GUI, in the study results page in the 'Last Seen' row. This way you can easily see if a worker is still running your study or if (and when) he abandonend it. By default the heartbeat period is 2 min. By careful not to set the period too low (few seconds or milliseconds) since it might overload your network or your JATOS server.

* _param {Number} heartbeatPeriod_ - Time period between two heartbeats in milliseconds


## Functions to control study flow

### `jatos.startComponent(componentId)`

Starts the component with the given ID. You can pass on information to the next component by adding a query string.

* _param {Object} componentId_ - ID of the component to start

### `jatos.startComponentByPos(componentPos)`

Starts the component with the given position (# of component within study). 

* _param {Object} componentPos_ - Position of the component to start

### `jatos.startNextComponent()`

Starts the next component of this study. The next component is the one with position + 1. 

### `jatos.startLastComponent()`

Starts the last component of this study or if it's inactive the component with the highest position that is active.

### `jatos.endComponent(successful, errorMsg, onSuccess, onError)`

Finishes component. Usually this is not necessary because the last component is automatically finished if the new component is started. Nevertheless it's useful to explicitly tell about a FAIL and submit an error message. Finishing the component doesn't finish the study.

* _param {optional Boolean} successful_ - 'true' if study should finish successful and the participant should get the confirmation code - 'false' otherwise.
* _param {optional String} errorMsg_ - Error message that should be logged.
* _param {optional Function} onSuccess_ - Function to be called in case of successful submit
* _param {optional Function} onError_ - Function to be called in case of error

### `jatos.abortStudyAjax(message, success, error)`

Aborts study. All previously submitted data will be deleted.

* _param {optional String} message_ - Message that should be logged
* _param {optional Function} success_ - Function to be called in case of successful submit
* _param {optional Function} error_ - Function to be called in case of error

### `jatos.abortStudy(message)`

Aborts study. All previously submitted data will be deleted.

* _param {optional String} message_ - Message that should be logged

### `jatos.endStudyAjax(successful, errorMsg, onSuccess, onError)`

Ends study with an Ajax call.

* _param {optional Boolean} successful_ - 'true' if study should finish successful and the participant should get the confirmation code - 'false' otherwise.
* _param {optional String} errorMsg_ - Error message that should be logged.
* _param {optional Function} onSuccess_ - Function to be called in case of successful submit
* _param {optional Function} onError_ - Function to be called in case of error

### `jatos.endStudy(successful, errorMsg)`

Ends study.

* _param {optional Boolean} successful_ - 'true' if study should finish successfully, 'false' otherwise.
* _param {optional String} errorMsg_ - Error message that should be logged.


## Functions for session and result

### `jatos.submitResultData(resultData, onSuccess, onError)`

Posts resultData back to the JATOS server.

* _param {Object} resultData_ - String to be submitted
* _param {optional Function} success_ - Function to be called in case of successful submit
* _param {optional Function} error_ - Function to be called in case of error

### `jatos.setStudySessionData(sessionData, complete)`

Posts study session data to the JATOS server. This function is called automatically in the end of a component's life cycle (it's called by all jatos.js functions that start or end a component). So unless you want to store the session data in between a component run it's not necessary to call this function manually (in opposite to the group session's _jatos.setGroupSessionData_).

* _param {Object} sessionData_ - Object to be submitted
* _param {optional Function} complete_ - Function to be called after this function is finished


## Functions for group studies

### `jatos.joinGroup(callbacks)`

Tries to join a group (actually a group result) and if it succeeds opens the group channel's WebSocket.

* _param {Object} callbacks_ - Defining callback functions for group events. All callbacks are optional. These callbacks functions can be:
  * **onOpen**: Is called when the group channel is successfully opened
  * **onClose**: Is be called when the group channel is closed
  * **onError**: Is called if an error during opening of the group channel's WebSocket occurs or if an error is received via the group channel (e.g. the group session data couldn't be updated). If this function is not defined jatos.js will try to call the global _onJatosError_ function.
  * **onMessage(msg)**: Is called if a message from another group member is received. It gets the message as a parameter.
  * **onMemberJoin(memberId)**: Is called when another member (not the worker running this study) joined the group. It gets the group member ID as a parameter.
  * **onMemberOpen(memberId)**: Is called when another member (not the worker running this study) opened a group channel. It gets the group member ID as a parameter.
  * **onMemberLeave(memberId)**: Is called when another member (not the worker running his study) left the group. It gets the group member ID as a parameter.
  * **onMemberClose(memberId)**: Is called when another member (not the worker running this study) closed his group channel. It gets the group member ID as a parameter.
  * **onGroupSession(groupSessionData)**: Is called when the group session is updated. It gets the new group session data as a parameter.
  * **onUpdate()**: Combines several other callbacks. It's called if one of the following is called: _onMemberJoin_, _onMemberOpen_, _onMemberLeave_, _onMemberClose_, or _onGroupSession_ (the group session can then be read via _jatos.groupSessionData_).

### `jatos.sendGroupMsg(msg)`

Sends a message to all group members with an open group channel. Like with most transmissions in the Internet these messages are send on a best effort basis. This means that if everything (e.g. network, browser, script) works fine the message gets delivered - but if the message transmission encounters a problem and is not delivered neither the sender nor the receiver will be notified. If you want more reliable message transmission use the group session and _jatos.setGroupSessionData_ instead. Compared to the transmission via group session the group messaging is fast but less reliable. 

* _param {Object} msg_ - Any JavaScript object

### `jatos.sendGroupMsgTo(recipient, msg)`

Sends a message to a single group member specified with the given group member ID (only if group channel is open).

* _param {String} recipient_ - Recipient's group member ID
* _param {Object} msg_ - Any JavaScript object

### `jatos.leaveGroup(onSuccess, onError)`

Tries to leave the group (actually a group result) it has previously joined. The group channel is not closed in this function - it's closed from the JATOS' side.

* _param {optional Function} onSuccess_ - Function to be called after the group is left
* _param {optional Function} onError_ - Function to be called in case of error

### `jatos.reassignGroup(onSuccess, onFail)`

Asks the JATOS server to reassign this study run to a different group.

* _param {optional Function} onSuccess_ - Function to be called if the reassignment was successful
* _param {optional Function} onFail_ - Function to be called if the reassignment was unsuccessful

### `jatos.setGroupSessionData(groupSessionData, onError)`

Sends the group session data via the group channel to the JATOS server where it's stored and broadcasted to all members of this group. It either takes an Object as parameter or uses _jatos.groupSessionData_ if the groupSessionData isn't provided. jatos.js tries several times to upload the session data, but if there are many concurrent members updating at the same time it might fail. But jatos.js/JATOS guarantees that it either persists the updated session data or calls the _onError_ callback. In this way it is more reliable but slower compared to _jatos.sendGroupMsg_ or _jatos.sendGroupMsgTo_. Since the group session is stored in the JATOS server it can be retrieved after a page reload or Internet connection problem to continue at the point of the interruption.

* _param {optional Object} groupSessionData_ - An object in JSON; If it's not given take _jatos.groupSessionData_
* _param {optional Object} onError_ - Function to be called if this upload was unsuccessful

### `jatos.setGroupFixed()`

Ask the JATOS server to fix this group. A fixed group is not allowed to take on more members although members are still allowed to leave.

### `jatos.hasJoinedGroup()`

Returns true if this study run joined a group and false otherwise. It doesn't necessarily mean that we have an open group channel. We can have joined a group in a prior component. If you want to check for an open group channel use _jatos.hasOpenGroupChannel_.

### `jatos.hasOpenGroupChannel()`

Returns true if we currently have an open group channel and false otherwise. Since you can't open a group channel without joining a group, it also means that we joined a group.

### `jatos.isMaxActiveMemberReached()`

Returns true if the group has reached the maximum amount of active members like specified in the batch properties. It's not necessary that each member has an open group channel.

### `jatos.isMaxActiveMemberOpen()`

Returns true if the group has reached the maximum amount of active members like specified in the batch properties and each member has an open group channel.

### `jatos.isGroupOpen()`

Returns true if all active members of the group have an open group channel. It's not necessary that the group has reached its minimum or maximum active member size.

