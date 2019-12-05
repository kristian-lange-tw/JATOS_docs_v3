---
title: jatos.js Reference
keywords: reference, jatos.js, function, variable, js, javascript, library
tags:
summary: jatos.js is a JavaScript library that helps you to communicate from your component's JavaScript with your JATOS server. Below we list and describe the variables and functions of the jatos.js library.
sidebar: mydoc_sidebar
permalink: jatos.js-Reference.html
folder:
toc: true
last_updated: 27 Nov 2019
---

Have a look at what's [mandatory in HTML and JavaScript for JATOS components](Mandatory-lines-in-your-components-HTML.html). Always load the jatos.js script in the `<head>` section with the following line:

```
<script src="jatos.js"></script>
```

or in older JATOS versions with:

```
<script src="/assets/javascripts/jatos.js"></script>
```

All variables or calls to jatos.js start with `jatos.`. For example, if you want to get the study's ID you use `jatos.studyId`. 

And, please, if you find a mistake or have a question don't hesitate to [contact us](Contact-us.html).


## jatos.js variables

You can call any of these variables below at any point in your HTML file after jatos.js finished initializing (`jatos.onLoad()` will be called). Most variables are read-only. A few variables can be written into (e.g. `jatos.httpTimeout`). Those are marked '(writeable)'.


### IDs

All those IDs are generated and stored by JATOS. jatos.js automatically sets these variables with the corresponding values if you included the `jatos.onLoad()` callback function at the beginning of your JavaScript.

* `jatos.studyId` - ID of the study which is currently running. All the study properties are associated with this ID.
* `jatos.componentId` - ID of the component which is currently running. All the component properties are associated with this ID.
* `jatos.batchId` - ID of the batch this study run belongs to. All batch properties are associated with this ID.
* `jatos.workerId` - Each worker who is running a study has an ID.
* `jatos.studyResultId` - This ID is individual for every study run. A study result contains data belonging to the run in general (e.g. Study Session).
* `jatos.componentResultId` - This ID is individual for every component in a study run. A component result contains data of the run belonging to the specific component (e.g. result data).
* `jatos.groupMemberId` - see [Group Variables](#group-variables)
* `jatos.groupResultId` - see [Group Variables](#group-variables)

There's a convenient function that adds all these IDs to a given object. See function `jatos.addJatosIds(obj)` below.


### Study variables

* `jatos.studyProperties` - All the properties (except the JSON input data) you entered for this study
  * `jatos.studyProperties.title` - Study's title
  * `jatos.studyProperties.uuid` - Study's UUID
  * `jatos.studyProperties.description` - Study's description
  * `jatos.studyProperties.descriptionHash` - Hash of study's description
  * `jatos.studyProperties.locked` - Whether the study is locked or not
  * `jatos.studyProperties.dirName` - Study's dir name in the file system of your JATOS installation
  * `jatos.studyProperties.groupStudy` - Whether this is a group study or not
* `jatos.studyJsonInput` - The JSON input you entered in the study's properties.
* `jatos.studyLength` - Number of component this study has


### Original URL query parameters

* `jatos.urlQueryParameters` - Original query string parameters of the URL that starts the study. It is provided as a JavaScript object. This might be useful to pass on information from outside of JATOS into a study run, e.g. if you want to pass on information like gender and age. However if you know the information beforehand it's easier to put them in the Study's or Component's JSON input. Another example is MTurk which passes on it's worker's ID via a URL query parameter.

  Example: One has this link to start a Personal Single Run:
  
  `http://localhost:9000/publix/50/start?batchId=47&personalSingleWorkerId=506`
  
  Now one could add parameters to the URL's query string to pass on external information into the study run. E.g. the following URL would add the parameters 'foo' with the value 'bar' and 'a' with the value '123':
  
  `http://localhost:9000/publix/50/start?batchId=47&personalSingleWorkerId=506&foo=bar&a=123`
  
  Then those parameter will be accessible during the study run in `jatos.urlQueryParameters` as `{a: "123", foo: "bar"}`.

  Example: MTurk uses for its worker ID the URL query parameter 'workerId' and this is accessible via `jatos.urlQueryParameters.workerId`.


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

The session data can be accessed and modified by every component of a study. It's a very convenient way to share data between different components. Whatever is written in this variable will be available in the subsequent components. However, remember that the session data will be deleted after the study is finished (see also [Session Data - Three Types](Session-Data-Three-Types.html)).

* `jatos.studySessionData` (writeable)


### Batch variables

* `jatos.batchProperties` - All the properties you entered for this batch.
  * `jatos.batchProperties.allowedWorkerTypes` - List of worker types that are currently allowed to run in this batch.
  * `jatos.batchProperties.maxActiveMembers` - How many members this group can have at the same time
  * `jatos.batchProperties.maxTotalMembers` - How many members this group is allowed to have at the same time
  * `jatos.batchProperties.maxTotalWorkers` - Total amount of workers this group is allowed to have altogether in this batch
  * `jatos.batchProperties.title` - Title of this batch
* `jatos.batchJsonInput` - The JSON input you entered in the batch's properties.


### Group variables

The group variables are part of jatos.js since JATOS 2. They are only filled with values if the current study is a group study.

* `jatos.groupMemberId` - Group member ID is unique for this member (it is actually identical with the study result ID)
* `jatos.groupResultId` - ID of this group result (It's called group result to be consistent with the study result and the component result - although often it's just called group)
* `jatos.groupState` (Removed in JATOS >= v3.4.1) - Represents the state of the group in JATOS; only set if group channel is open (one of STARTED, FIXED, FINISHED)
* `jatos.groupMembers` - List of member IDs of the current members of the group
* `jatos.groupChannels` - List of member IDs of the currently open group channels


### Other variables

All variables can be set except those labled _read-only_.

* `jatos.version` (_read-only_) - Current version of the jatos.js library
* `jatos.channelSendingTimeoutTime` - Time in ms to wait for an answer after sending a message via a channel (batch or group). Set this variable if you want to change the default value (default is 10 s).

  ```javascript
  jatos.channelSendingTimeoutTime = 20000; // Sets channel timeout to 20 seconds
  ```
  
* `jatos.channelHeartbeatInterval` -  Waiting time in ms between channel (group or batch) heartbeats (default is 25 s)
  
  ```javascript
  jatos.channelHeartbeatInterval = 10000; // Sets interval to 10 seconds
  ```
  
* `jatos.channelHeartbeatTimeoutTime` - Waiting time in ms for JATOS server's answer to a channel heartbeat (default is 10 s)
  
  ```javascript
  jatos.channelHeartbeatTimeoutTime = 20000; // Sets interval to 20 seconds
  ```
  
* `jatos.channelClosedCheckInterval` - Waiting time in ms between checking if channels (group or batch) are closed unexpectedly (default is 2 s)
  
  ```javascript
  jatos.channelClosedCheckInterval = 4000; // Sets interval to 4 seconds
  ```
  
* `jatos.channelOpeningBackoffTimeMin` and `jatos.channelOpeningBackoffTimeMax` - Min and max waiting time (in ms) between channel reopening attempts (default is 1s for min and 2 min for max). jatos.js uses an _exponential back-off_ retry pattern for the channels.
  
  ```javascript
  jatos.channelOpeningBackoffTimeMin = 2000; // Sets interval to 2 seconds
  jatos.channelOpeningBackoffTimeMax = 60000; // Sets interval to 1 minute
  ```

* `jatos.httpTimeout` - Time in ms to wait for an answer of an HTTP request by jatos.js. Set this variable if you want to change the default value (default is 1 min).

  ```javascript
  jatos.httpTimeout = 30000; // Sets HTTP timeout to 30 seconds
  ```
  
* `jatos.httpRetry` - Some jatos functions (e.g. `jatos.sendResultData`) send an Ajax request to the JATOS server. If this request was not successful (e.g. network problems) jatos.js retries it. With this variable one can change the number of retries. The default is 5. 

  ```javascript
  jatos.httpRetry = 2; // Attempts 2 retries of failed Ajax requests
  ```
  
* `jatos.httpRetryWait` - Same as `jatos.httpRetry` but this variable defines the waiting time between the retries. The default is 1000 ms.
  
  ```javascript
  jatos.httpRetryWait = 5000; // Sets Ajax retry waiting time to 5 seconds
  ```

* `jatos.jQuery` (_read-only_) - You can always use jatos.js own jQuery if you want to save some bandwidth



## General jatos.js functions

### `jatos.onLoad`

Defines callback function that jatos.js will call when it's finished initialising. Only [mandatory](Mandatory-lines-in-your-components-HTML.html) call in every component.

* @param {function} callback - function to be called after jatos.js' initialization is done

**Example**

```javascript
jatos.onLoad(function() {
  // Start here with your code that uses jatos.js' variables and functions
});
```


### `jatos.onError`

Defines a callback function that is to be called in case jatos.js produces an error. 

* @param {function} callback - Function to be called in case of an error

**Example**

Show the error message in an alert box:

```javascript
jatos.onError(alert);
```


### `jatos.log`

Sends a message to be logged back to the JATOS server where it will be logged in JATOS' log file.

* _@param {string} logMsg_ - The messages to be logged  

**Example**

```javascript
jatos.log("Log this message in JATOS' log file");
```


### `jatos.addJatosIds`

Convenience function that adds some [IDs](jatos.js-Reference.html#ids) (study ID, study title, batch ID, batch title, component ID, component position, component title, worker ID, study result ID, component result ID, group result ID, group member ID) to the given object.

* _@param {object} obj_ - Object to which the IDs will be added

**Example**

```javascript
var resultData = {};
jatos.addJatosIds(resultData);
```


### `jatos.setHeartbeatPeriod`

Every running component sends regularly a HTTP request (the heartbeat) back to the JATOS server. This signals that it is still running. As soon as the browser tab running the component is closed the heartbeat ceases. The time of the last heartbeat is visible in the GUI, in the study results page in the 'Last Seen' row. This way you can easily see if a worker is still running your study or if (and when) he abandonend it. By default the heartbeat period is 2 minutes. By careful not to set the period too low (few seconds or even milliseconds) since it might overload your network or your JATOS server.

* _@param {number} heartbeatPeriod_ - Time period between two heartbeats in milliseconds

**Example**

```javascript
jatos.setHeartbeatPeriod(60000); // Sets to a heartbeat every minute
```


## Functions to control study flow

### `jatos.startComponent`

Finishes the currently running component and starts the component with the given ID. Though often it's better to use `jatos.startComponentByPos` instead because it keeps working even after an export/import of the study into another JATOS. Since v3.3.1 one can additionally send result data back to the JATOS server.

Since v3.4.1 there are two version: with or without message

1. Without message:
	 * _@param {number} componentId_ - ID of the component to start
   * _@param {optional object} resultData_ - (JATOS >= v3.3.1) String or object that will be sent as result data. An object will be serialized to JSON (stringify). 
   * _@param {optional function} onError_ - Callback function if fail

1. With message (since JATOS >= v3.4.1):
	 * _@param {number} componentId_ - ID of the component to start
	 * _@param {optional object} resultData_ - String or object that will be sent as result data. An object will be serialized to JSON (stringify). 
	 * _@param {optional string} message_ - Message that should be logged (max 255 chars)
	 * _@param {optional function} onError_ - Callback function if fail

**Examples**

1. Jump to component with ID 23

   ```javascript
   jatos.startComponent(23);
   ```

1. Since v3.3.1: send result data and jump to another component

   ```javascript
   var resultData = "my important result data";
   jatos.startComponent(23, resultData);
   ```

1. Since v3.4.1: send result data, jump to another component and send a message back that will be visible in JATOS result pages and log 

   ```javascript
   var resultData = "my important result data";
   jatos.startComponent(23, resultData, "everything okay");
   ```

1. In versions < v3.3.1 it's often used together with `jatos.submitResultData` to first submit result data back to the JATOS server and afterwards jump to another component

   ```javascript
   var resultData = "my important result data";
   jatos.submitResultData(resultData, function() {
     jatos.startComponent(23);
   });
   ```


### `jatos.startComponentByPos`

Finishes the currently running component and starts the component with the given position. The component position is the count of the component within the study like shown in the study overview page (1st component has position 1, 2nd component position 2, ...). Since v3.3.1 one can additionally send result data back to the JATOS server.

Since v3.4.1 there are two versions: with or without message

1. Without message

   * _@param {number} componentPos_ - Position of the component to start
   * _@param {optional object} resultData_ - (JATOS >= v3.3.1) String or object that will be sent as result data. An object will be serialized to JSON (stringify). 
   * _@param {optional function} onError_ - Callback function if fail

1. With message (since JATOS >= v3.4.1)

   * _@param {number} componentPos_ - Position of the component to start
	 * _@param {optional object or string} resultData_ - String or object that will be sent as result data. An object will be serialized to JSON (stringify). 
	 * _@param {optional string} message_ - Message that should be logged (max 255 chars)
	 * _@param {optional function} onError_ - Callback function if fail

**Examples**

1. Jump to component in position 3

   ```javascript
   jatos.startComponentByPos(3);
   ```

1. Since v3.3.1: send result data and jump to component with position 3

   ```javascript
   var resultData = "my important result data";
   jatos.startComponentByPos(3, resultData);
   ```

1. Since v3.4.1: send result data, jump to component in position 3 and send a message back that will be visible in JATOS result pages and log 

   ```javascript
   var resultData = "my important result data";
   jatos.startComponentByPos(3, resultData, "everything okay");
   ```

1. In versions < v3.3.1 it's often used together with `jatos.submitResultData` to first submit result data back to the JATOS server and afterwards jump to component in position 3

   ```javascript
   var resultData = "my important result data";
   jatos.submitResultData(resultData, function() {
     jatos.startComponentByPos(3);
   });
   ```


### `jatos.startNextComponent`

Finishes the currently running component and starts the next component of this study. The next component is the one with position + 1. The component position is the count of the component within the study like shown in the study overview page (1st component has position 1, 2nd component position 2, ...). Since v3.3.1 one can additionally send result data back to the JATOS server.

Since v3.4.1 there are two versions: with or without message

1. Without message

   * _@param {optional object} resultData_ - (JATOS >= v3.3.1) String or object that will be sent as result data. An object will be serialized to JSON (stringify). 
   * _@param {optional function} onError_ - Callback function if fail

1. With message (since JATOS >= v3.4.1)

	 * _@param {optional object or string} resultData_ - String or object that will be sent as result data. An object will be serialized to JSON (stringify). 
	 * _@param {optional string} message_ - Message that should be logged (max 255 chars)
	 * _@param {optional function} onError_ - Callback function if fail

**Examples**

1. Jump to the next component

   ```javascript
   jatos.startNextComponent();
   ```

1. Since v3.3.1: send result data and jump to the next component

   ```javascript
   var resultData = "my important result data";
   jatos.startNextComponent(resultData);
   ```

1. Since v3.4.1: send result data, jump to the next component and send a message back that will be visible in JATOS result pages and log 

   ```javascript
   var resultData = "my important result data";
   jatos.startNextComponent(resultData, "everything okay");
   ```

1. In versions < v3.3.1 it's often used together with `jatos.submitResultData` to first submit result data back to the JATOS server and afterwards jump to the next component

   ```javascript
   var resultData = "my important result data";
   jatos.submitResultData(resultData, jatos.startNextComponent);
   ```


### `jatos.startLastComponent`

Finishes the current component and starts the last component of this study. If the last component is inactive it starts the component with the highest position that is active. The component position is the count of the component within the study like shown in the study overview page (1st component has position 1, 2nd component position 2, ...). Since v3.3.1 one can additionally send result data back to the JATOS server.

Since v3.4.1 there are two versions: with or without message

1. Without message

	 * _@param {optional object} resultData_ - (JATOS >= v3.3.1) String or object that will be sent as result data. An object will be serialized to JSON (stringify). 
   * _@param {optional function} onError_ - Callback function if fail

1. With message (since JATOS >= v3.4.1)

	 * _@param {optional object or string} resultData_ - String or object that will be sent as result data. An object will be serialized to JSON (stringify). 
	 * _@param {optional string} message_ - Message that should be logged (max 255 chars)
	 * _@param {optional function} onError_ - Callback function if fail

**Examples**

1. Jump to the last component

   ```javascript
   jatos.startLastComponent();
   ```

1. Since v3.3.1: send result data and jump to the last component

   ```javascript
   var resultData = "my important result data";
   jatos.startLastComponent(resultData);
   ```

1. Since v3.4.1: send result data, jump to the last component and send a message back that will be visible in JATOS result pages and log

   ```javascript
   var resultData = "my important result data";
   jatos.startLastComponent(resultData, "everything okay");
   ```


1. In versions < v3.3.1 it's often used together with `jatos.submitResultData` to first submit result data back to the JATOS server and afterwards jump to the last component

   ```javascript
   var resultData = "my important result data";
   jatos.submitResultData(resultData, jatos.startLastComponent);
   ```


### `jatos.abortStudy`

Aborts study. All previously submitted result data will be deleted. Afterwards the worker is redirected to the study end page. Data stored in the Batch Session or Group Session are uneffected by this.

* _@param {optional string} message_ - Message that will be stored together with the study results and is accessible via JATOS' GUI result pages. The message can be max 255 characters long.
* _@param {optional boolean} showEndPage_ - If 'true' an end page is shown - if 'false' it	behaves like `jatos.endStudyAjax`, which means no showing of JATOS' end page

**Examples**

1. Just abort study

   ```javascript
   jatos.abortStudy();
   ```

1. Additionally send a message

   ```javascript
   jatos.abortStudy("participant aborted by pressing abort button");
   ```


### `jatos.abortStudyAjax`

Aborts study with an Ajax call. All previously submitted result data will be deleted. Data stored in the Batch Session or Group Session are uneffected by this. It offers callbacks, either as parameter or via [jQuery.deferred.promise](https://api.jquery.com/deferred.promise/), to signal success or failure in the ending.

* _@param {optional string} message_ - Message that should be logged
* _@param {optional function} onSuccess_ - Function to be called in case of successful submit
* _@param {optional function} onError_ - Function to be called in case of error
* _@return {jQuery.deferred.promise}_

**Examples**

1. Just abort study

   ```javascript
   jatos.abortStudyAjax();
   ```

1. Abort study with a message that will be sent back to JATOS and shown in the result page and put in the log

   ```javascript
   jatos.abortStudyAjax("Worker clicked Abort button");
   ```


### `jatos.endStudy`

Ends study. Redirects the worker to study's end page afterwards.

Since v3.4.1 there are two versions: with and without result data

1. With result data (since JATOS >= v3.4.1)
	  * _@param {optional string or object} resultData_ - Result data to be sent back	to JATOS server
	  * _@param {optional boolean} successful_ - 'true' if study should finish successfully, 'false' otherwise. Default is true
	  * _@param {optional string} message_ - Message that will be stored together with the study results and is accessible via JATOS' GUI result pages. The message can be max 255 characters long
	  * _@param {optional boolean} showEndPage_ - If 'true' an end page is shown - if 'false' it	behaves like `jatos.endStudyAjax`, which means no showing of JATOS' end page

1. Without result data
	  * _@param {optional boolean} successful_ - 'true' if study should finish successfully, 'false' otherwise. Default is true
	  * _@param {optional string} message_ - Message that will be stored together with the study results and is accessible via JATOS' GUI result pages. The message can be max 255 characters long
	  * _@param {optional boolean} showEndPage_ - If 'true' an end page is shown - if 'false' it	behaves like `jatos.endStudyAjax`, which means no showing of JATOS' end page

**Examples**

1. Just end study

   ```javascript
   jatos.endStudy();
   ```

1. End study and send a message back that will be visible in JATOS result pages and log 

   ```javascript
   jatos.endStudy("everything worked fine");
   ```

1. Indicate a failure - leads to study result state FAIL

   ```javascript
   jatos.endStudy(false, "internal JS error");
   ```

1. Send result data and end study (since JATOS >= v3.4.1)

   ```javascript
   var resultData = {id: 123, data: "my important result data"};
   jatos.endStudy(resultData);
   ```

1. Send result data, end study and send a message back that will be visible in JATOS result pages and log (since JATOS >= v3.4.1)

   ```javascript
   var resultData = {id: 123, data: "my important result data"};
   jatos.endStudy(resultData, "everything worked fine");
   ```


### `jatos.endStudyAjax`

Ends study with an Ajax call - afterwards the study is not redirected to the JATOS' end page. It offers callbacks, either as parameter or via [jQuery.deferred.promise](https://api.jquery.com/deferred.promise/), to signal success or failure in the ending.

* _@param {optional boolean} successful_ - 'true' if study should finish successful and the participant should get the confirmation code - 'false' otherwise.
* _@param {optional string} message_ - Message that will be stored together with the study results and is accessible via JATOS' GUI result pages. The message can be max 255 characters long.
* _@param {optional function} onSuccess_ - Function to be called in case of successful submit
* _@param {optional function} onError_ - Function to be called in case of error
* _@return {jQuery.deferred.promise}_

**Examples**

1. Just end study

   ```javascript
   jatos.endStudyAjax();
   ```

1. End study with a message that will be sent back to JATOS and shown in the result page and put in the log

   ```javascript
   jatos.endStudyAjax("everything worked fine");
   ```

1. Indicate a failure and send a message

   ```javascript
   jatos.endStudyAjax(false, "internal JS error");
   ```

1. Send result data, end study and jump to another URL afterwards (by using jQuery's [done](https://api.jquery.com/deferred.done/)

   ```javascript
   var resultData = {id: 123, data: "my important result data"};
   jatos.submitResultData(resultData)
     .done(jatos.endStudyAjax)
     .done(() => {
       window.location.href = 'http://example.com/index.html'
    });
   ``` 

1. Send result data and end study (since JATOS >= v3.4.1)

   ```javascript
   var resultData = {id: 123, data: "my important result data"};
   jatos.endStudy(resultData);
   ```    


## functions for Study Session and result data

### `jatos.submitResultData`

Posts result data for the currently running component back to the JATOS server. Already stored result data for this component will be **overwritten**. If you want to append result data use `jatos.appendResultData` instead. Alternatively you can send result data with functions that jump to another component (e.g. `jatos.startComponent`) or end the study (`jatos.endStudy`). It offers callbacks, either as parameter or via [jQuery.deferred.promise](https://api.jquery.com/deferred.promise/), to signal success or failure in the transfer.

* _@param {object} resultData_ - String or object that will be sent as result data. An object will be serialized to JSON.
* _@param {optional function} onSuccess_ - Function to be called in case of successful submit
* _@param {optional function} onError_ - Function to be called in case of error
* _@return {jQuery.deferred.promise}_

**Examples**

1. Send result data back to the JATOS server

   ```javascript
   var resultData = {"a": 123, "b": 789, "c": 100};
   jatos.submitResultData(JSON.stringify(resultData));
   ```

1. Since v3.3.1 it's possible to leave out the JSON serialization

   ```javascript
   var resultData = {"a": 123, "b": 789, "c": 100};
   jatos.submitResultData(resultData);
   ```

1. It's often used together with `jatos.startNextComponent` to first submit result data back to the JATOS server and afterwards jump to the next component

   ```javascript
   var resultData = {"a": 123, "b": 789, "c": 100};
   jatos.submitResultData(resultData, jatos.startNextComponent);
   ```


1. Or together with `jatos.startComponentByPos` to start a particular component (here at position 4)

   ```javascript
   var resultData = {"a": 123, "b": 789, "c": 100};
   jatos.submitResultData(resultData, () => { jatos.startComponentByPos(4) });
   ```

1. Or with jQuery's [then](https://api.jquery.com/deferred.then/) function

   ```javascript
   var resultData = {"a": 123, "b": 789, "c": 100};
   jatos.submitResultData(resultData).then(() => console.log('success'), () => console.log('error'));
   ```


### `jatos.appendResultData`

**Since JATOS version >= 3.1.7** - Appends result data to the already posted result data. Contrary to `jatos.submitResultData` it does not overwrite the result data. Alternatively you can send result data with functions that jump to another component (e.g. `jatos.startComponent`) or end the study (`jatos.endStudy`). It offers callbacks, either as parameter or via [jQuery.deferred.promise](https://api.jquery.com/deferred.promise/), to signal success or failure in the transfer. This function can be used several times during an component run to incrementally save result data.

* _@param {string} resultData_ - String or object that will be sent as result data. An object will be serialized to JSON (stringify).
* _@param {optional function} onSuccess_ - Function to be called in case of successful submit
* _@param {optional function} onError_ - Function to be called in case of error
* _@return {jQuery.deferred.promise}_

**Examples**

1. Append result data to the already sent

   ```javascript
   var resultData = { "a": 123, "b": 789, "c": 100};
   jatos.appendResultData(JSON.stringify(resultData));
   ```

1. Since v3.3.1 it's possible to leave out the JSON serialization

   ```javascript
   var resultData = {"a": 123, "b": 789, "c": 100};
   jatos.appendResultData(resultData);
   ```

1. You can use it together with `jatos.startNextComponent` to first append result data and afterwards jump to the next component

   ```javascript
   var resultData = { "a": 123, "b": 789, "c": 100};
   jatos.appendResultData(resultData, jatos.startNextComponent);
   ```

1. Or together with `jatos.startComponentByPos` to start a particular component (here at position 4)

   ```javascript
   var resultData = { "a": 123, "b": 789, "c": 100};
   jatos.appendResultData(resultData, () => { jatos.startComponentByPos(4) });
   ```


### `jatos.setStudySessionData`

**If you just want to write into the study session, this function is not what you want**. This function sets the study session data and **sends it back to the JATOS server**. If you want to write something into the study session, just write into the [`jatos.studySessionData`](jatos.js-Reference.html#studys-session-data) variable.

Posts Study Session data to the JATOS server. This function is called automatically in the end of a component's life cycle (it's called by all jatos.js functions that end a component). So unless you want to store the session data during a component run yourself, **it's not necessary to call this function manually**. It offers callbacks, either as parameter or via [jQuery.deferred.promise](https://api.jquery.com/deferred.promise/), to signal success or failure in the transfer.

* _@param {object} sessionData_ - object to be submitted
* _@param {optional function} onSuccess_ - Function to be called after this function is finished
* _@param {optional function} onFail_ - Function to be called after if this this functions fails
* _@return {jQuery.deferred.promise}_

**Example**

```javascript
var studySessionData = { "a": 123, "b": 789, "c": 100};
jatos.setStudySessionData(studySessionData);
```


## Functions to access the Batch Session

The Batch Session is stored in JATOS' database on the server side (see also [Session Data - Three Types](Session-Data-Three-Types.html)). That means that all changes in the Batch Session have to be synchronized between the client and the server. This is done via the batch channel. Therefore all writing functions (`add`, `remove`, `clear`, `replace`, `copy`, `move`, `set`, `setAll`) can be paired with callback functions that will signal  success or failure in the client-server sync. These callback functions can be either passed as parameters to `jatos.batchSession.[function_name]` or via [jQuery.deferred.promise](https://api.jquery.com/deferred.promise/).

On the other side for all reading functions (`get`, `find`, `getAll`, `test`) there is no need to sync data between client and server, because jatos.js keeps a copy of the Batch Session locally. Therefore all reading functions do not offer callbacks, because there is no risk of failure of synchronization.

Additionally to the reading and writing functions the calback function `jatos.onBatchSession(callback)` offers a way to get notified whenever the Batch Session changes in the JATOS' database regardless of the origin of the change. This way, you can have the client of each worker react to changes in the batch that were done by another worker in the batch. 

Accessing the Batch Session is done via [JSON Patches (RFC 6902)](https://tools.ietf.org/html/rfc6902) and 
[JSON Pointer (RFC 6901)](https://tools.ietf.org/html/rfc6901). An introduction can be found under [jsonpatch.com](http://jsonpatch.com/). For JSON Patches jatos.js uses the [JSON-Patch](https://github.com/Starcounter-Jack/JSON-Patch) library from Joachim Wester and for JSON Pointers the [jsonpointer.js](https://github.com/alexeykuzmin/jsonpointer.js) library from Alexey Kuzmin.


### `jatos.batchSession.add`

JSON Patch add operation: Adds a value to an object or inserts it into an array. In the case of an array, the value is inserted before the given index. The `-` character can be used instead of an index to insert at the end of an array (see [jsonpatch.com](http://jsonpatch.com/)). If the path already exists in the Batch Session the value will be overwritten.

* _@param {string} path_ - JSON pointer path 
* _@param {object} value_ - value to be stored
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

**Examples**

1. Add to Batch Session

   If the Batch Session is `{"a": 100}` and one calls

   ```javascript
   jatos.batchSession.add("/b", 123);
   ```

   then after the Batch Session is successfully updated the new object is `{"a": 100, "b": 123}`.

   Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

1. Catch failures with jQuery's defered

   ```javascript
   var deferred = jatos.batchSession.add("/b", 123);
   deferred.done(() => { alert("Batch Session was successfully updated") });
   deferred.fail(() => { alert("Batch Session synchronization failed") });
   ```

1. Example with an array: Put the object `{id: 123, name: "Max"}` after the second position of the array with the path `/subjects`

   ```javascript
   var deferred = jatos.batchSession.add("/subjects/2", {id: 123, name: "Max"});
   deferred.done(() => { alert("Batch Session was successfully updated") });
   deferred.fail(() => { alert("Batch Session synchronization failed") });
   ```

1. Append to the end of an array use `/-` after the arrays name:

   ```javascript
   var deferred = jatos.batchSession.add("/subjects/-", {id: 124, name: "Adam"});
   deferred.done(() => { alert("Batch Session was successfully updated") });
   deferred.fail(() => { alert("Batch Session synchronization failed") });
   ```


### `jatos.batchSession.remove`

JSON Patch remove operation: Removes a value from an object or array (see [jsonpatch.com](http://jsonpatch.com/)).

* _@param {string} path_ - JSON pointer path to the field that should be removed
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

**Examples**

1. Remove from the Batch Session

   If the Batch Session is `{"a": 100, "b": 123}` and one calls

   ```javascript
   jatos.batchSession.remove("/b");
   ```

   then after the Batch Session is successfully updated the new object is `{"a": 100}`.

   Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

1. Catch failures with jQuery's defered

   ```javascript
   var deferred = jatos.batchSession.remove("/b");
   deferred.done(() => { alert("Batch Session was successfully updated") });
   deferred.fail(() => { alert("Batch Session synchronization failed") });
   ```


### `jatos.batchSession.replace`

JSON Patch replace operation: Replaces a value. Equivalent to a 'remove' followed by an 'add' (see [jsonpatch.com](http://jsonpatch.com/)).

* _@param {string} path_ - JSON pointer path 
* _@param {object} value_ - value to be replaced with
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

**Examples**

1. Replace in the Batch Session

   If the Batch Session is `{"a": 100, "b": 123}` and one calls

   ```javascript
   jatos.batchSession.replace("/b", 789);
   ```

   then after the Batch Session is successfully updated the new object is `{"a": 100, "b": 789}`.

   Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

1. Catch failures with jQuery's defered

   ```javascript
   var deferred = jatos.batchSession.replace("/b", 789);
   deferred.done(() => { alert("Batch Session was successfully updated") });
   deferred.fail(() => { alert("Batch Session synchronization failed") });
   ```


### `jatos.batchSession.copy`

JSON Patch copy operation: Copies a value from one location to another within the JSON document. Both from and path are JSON Pointers (see [jsonpatch.com](http://jsonpatch.com/)).

* _@param {string} from_ - JSON pointer path to the origin 
* _@param {string} path_ - JSON pointer path to the target
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

**Examples**

1. Copy within the Batch Session from one location to another

   If the Batch Session is `{"a": "jatos"}` and one calls

   ```javascript
   jatos.batchSession.copy("/a", "/b");
   ```

   then after the Batch Session is successfully updated the new object is `{"a": "jatos", "b": "jatos"}`.

   Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

1. Catch failures with jQuery's defered

   ```javascript
   var deferred = jatos.batchSession.copy("/a", "/b");
   deferred.done(() => { alert("Batch Session was successfully updated") });
   deferred.fail(() => { alert("Batch Session synchronization failed") });
   ```


### `jatos.batchSession.move`

JSON Patch move operation: Moves a value from one location to the other. Both from and path are JSON Pointers. (see [jsonpatch.com](http://jsonpatch.com/)).

* _@param {string} from_ - JSON pointer path to the origin 
* _@param {string} path_ - JSON pointer path to the target
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

**Example**

1. Move within the Batch Session from one location to another

   If the Batch Session is `{"a": "jatos"}` and one calls

   ```javascript
   jatos.batchSession.move("/a", "/b");
   ```

   then after the Batch Session is successfully updated the new object is `{"b": "jatos"}`.

   Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

1. Catch failures with jQuery's defered

   ```javascript
   var deferred = jatos.batchSession.move("/a", "/b");
   deferred.done(() => { alert("Batch Session was successfully updated") });
   deferred.fail(() => { alert("Batch Session synchronization failed") });
   ```


### `jatos.batchSession.find`

Gets a field in the Batch Session data. Takes a JSON Pointer and returns the matching value. Gets the object from the locally stored copy of the session and does not call the server. Contrary to `jatos.batchSession.get` it allows to get values from all levels of the Batch Session's object tree.

* _@param {string} path_ - JSON pointer path 
* _@return {object}_ - the value that is stored in path

**Example**

1. Find a field in the Batch Session

   If the Batch Session is `{"a": {"a1": "foo", "a2": "bar"}, "b": 999}`

   ```javascript
   jatos.batchSession.find("/a/a1"); // returns "foo"
   jatos.batchSession.find("/b"); // returns 999
   ```


### `jatos.batchSession.defined`

**Since JATOS version >= 3.1.8** - Checks in the Batch Session whether a field under the given path exists. Returns true if the field is defined and false otherwise. It's equivalent to `!jatos.batchSession.test(path, undefined)`.

* _@param {string} path_ - JSON pointer path to be checked
* _@return {boolean}_ - 'true' if the field is defined and 'false' otherwise

**Example**

```javascript
jatos.batchSession.defined("/a"); // returns true if the pointer '/a' exists
```


### `jatos.batchSession.test`

JSON Patch test operation: Tests that the specified value is set in the document (see [jsonpatch.com](http://jsonpatch.com/)).

* _@param {string} path_ - JSON pointer path to be tested
* _@param {object} value_ - value to be tested
* _@return {boolean}_

**Examples**

1. Test if a certain field in the Batch Session has a value

   If the Batch Session is `{"a": 123, "b": {"b1": "flowers", "b2": "animals"}}`

   ```javascript
   jatos.batchSession.test("/a", 123); // returns true
   jatos.batchSession.test("/a", 10); // returns false
   jatos.batchSession.test("/b/b1", "flowers"); // returns true
   ```

1. If you want to know the existence of a path in the Batch Session you can test against `undefined`:

   ```javascript
   if (!jatos.batchSession.test("/c", undefined)) {
     // Path "/c" exists
   } else {
     // Path "/c" doesn't exist
   }
   ```


### `jatos.batchSession.get`

Convenience function: like `jatos.batchSession.find` but works with a key instead of a JSON Pointer. Therefore it works only on the first level of the session's object tree. It takes a name of an field within the Batch Session and returns the matching value.  For all other levels of the object tree use jatos.batchSession.find. Gets the object from the locally stored copy of the session and does not call the server.

* _@param {string} name_ - name of the field 
* _@return {object}_ - the value that is stored under name

**Examples**

1. Get the value that belongs to a key in the Batch Session

   If the Batch Session is `{"a": 1000, "b": "watermelon"}`

   ```javascript
   // Since the parameter is the key's name and not a path it does not start with a "/"
   var b = jatos.batchSession.get("b"); // b is "watermelon"
   var c = jatos.batchSession.get("c"); // c is undefined
   ```

1. With `jatos.batchSession.get` you can only access the first level of the object tree - if you want another level use `jatos.batchSession.find`. If the Batch Session is `{"a": {"a1": 123, "a2": "watermelon"}}`

   ```javascript
   var a1 = jatos.batchSession.get("a1"); // a1 is undefined !!!
   var a = jatos.batchSession.get("a"); // a is { "a1": 123, "a2": "watermelon" }
   ```


### `jatos.batchSession.set`

A convenience function for `jatos.batchSession.add`. Instead of a JSON Pointer path it accepts a name of the field to be stored (without a slash in front). Therefore it works only on the first level of the Batch Session's object tree. If the name already exists in the Batch Session the value will be overwritten.

* _@param {string} name_ - name of the field 
* _@param {object} value_ - value to be stored
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

**Examples**

1. Set a key and its value in the Batch Session

   If the Batch Session is `{"a": 1234}`

   ```javascript
   // Since the parameter is the key's name and not a path it does not start with a "/"
   var b = jatos.batchSession.set("b", "koala");
   ```

   then after the Batch Session is successfully updated the new object is `{"a": 1234, "b": "koala"}`.

   Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

1. Catch failures with jQuery's defered

   ```javascript
   var deferred = jatos.batchSession.set("b", "koala");
   deferred.done(() => { alert("Batch Session was successfully updated") });
   deferred.fail(() => { alert("Batch Session synchronization failed") });
   ```


### `jatos.batchSession.getAll`

Returns the complete Batch Session data. Gets the object from the locally stored copy of the session and does not call the server.

* _@return {object}_ Returns the whole Batch Session object

**Example**

```javascript
var batchSession = jatos.batchSession.getAll();
```


### `jatos.batchSession.setAll`

Replaces the whole session data. If the replacing object is rather large it might be better performance-wise to replace only individual paths. Each session writting involves sending the changes in the session via a JSON Patch to the JATOS server. If the session is large this data transfer can take some time. In this case use other session functions, like 'set', 'add', or 'replace'.

* _@param {object} value_ - value to be stored in the session
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

**Examples**

1. Set the whole Batch Session object

   ```javascript
   var o = {"a": 123, "b": "foo"};
   jatos.batchSession.setAll(o); // Overwrites the current Batch Session with the object o
   ```

   Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

1. Catch failures with jQuery's defered

   ```javascript
   var o = {"a": 123, "b": "foo"};
   var deferred = jatos.batchSession.setAll(o);
   deferred.done(() => { alert("Batch Session was successfully updated") });
   deferred.fail(() => { alert("Batch Session synchronization failed") });
   ```


### `jatos.batchSession.clear`

Clears the whole Batch Session data and sets it to an empty object `{}`.

* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

**Examples**

1. Clear the whole Batch Session

   ```javascript
   jatos.batchSession.clear();
   ```

   Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

1. Catch failures with jQuery's defered

   ```javascript
   var deferred = jatos.batchSession.clear();
   deferred.done(() => { alert("Batch Session was successfully updated") });
   deferred.fail(() => { alert("Batch Session synchronization failed") });
   ```


### `jatos.onBatchSession`

Defines a callback function that is called every time the Batch Session changes on the JATOS server side (that includes updates in the session originating from other workers that run the study in parallel).

The callback function has two parameter (before v3.3.1 one parameter):
* _@param {string} path_ - JSON pointer to the changed field in the Batch Session
* _@param {string} op_ - (version >= 3.3.1) JSON patch operation ('add', 'remove', 'clear', ...) that was applied

**Examples**

1. Show an alert box whenever something changes in the Batch session

   ```javascript
   jatos.onBatchSession(function(path, op){
     alert("Batch Session was updated in path " + path + " with operation " + op);
   });
   ```

1. `onBatchSession` is often used together with `jatos.batchSession.find` to get the updated value:

   ```javascript
   jatos.onBatchSession(function(path){
     var changedObj = jatos.batchSession.find(path);
     alert("The changed object is " + JSON.stringify(changedObj));
   });
   ```


## Functions for group studies

### `jatos.joinGroup`

Tries to join a group and if it succeeds opens the group channel (which is mostly a WebSocket). Only if the group channel is open one can exchange data with other group members. As the only parameter this function takes an object that consists of several optional callback functions that will be called by jatos.js when certain group events occur. It returns a [jQuery.deferred.promise](https://api.jquery.com/deferred.promise/), to signal success or failure in joining.

* _@param {object} callbacks_ - Defining callback functions for group events. All callbacks are optional. These callbacks functions are:
  * `onOpen`: Is called when the group channel is successfully opened
  * `onClose`: Is be called when the group channel is closed
  * `onError`: Is called if an error during opening of the group channel's WebSocket occurs or if an error is received via the group channel (e.g. the Group Session data couldn't be updated). If this function is not defined jatos.js will try to call the global `onJatosError` function.
  * `onMessage(msg)`: Is called if a message from another group member is received. It gets the message as a parameter.
  * `onMemberJoin(memberId)`: Is called when another member (not the worker running this study) joined the group. It gets the group member ID as a parameter.
  * `onMemberOpen(memberId)`: Is called when another member (not the worker running this study) opened a group channel. It gets the group member ID as a parameter.
  * `onMemberLeave(memberId)`: Is called when another member (not the worker running his study) left the group. It gets the group member ID as a parameter.
  * `onMemberClose(memberId)`: Is called when another member (not the worker running this study) closed his group channel. It gets the group member ID as a parameter.
  * `onGroupSession(path, op)`: Is called every time the Group Session changes on the JATOS server side. It gets two parameters (before v3.3.1 only one): 1) JSON pointer path to the changed field in the Group Session as a parameter, and 2) JSON patch operation.
  * `onUpdate()`: Combines several other callbacks. It's called if one of the following is called: `onMemberJoin`, `onMemberOpen`, `onMemberLeave`, `onMemberClose`, or `onGroupSession`.
* _@return {jQuery.deferred.promise}_

**Examples**

1. Minimal example that joins a group and receives updates via the Group Session

   ```javascript
   jatos.joinGroup({
     "onGroupSession": onGroupSession
   });

   function onGroupSession(path, op) {
     var changedObj = jatos.groupSession.find(path);
     alert("Group Session was updated in path " + path + " with operation " + op + " to " + JSON.stringify(changedObj));
   }
   ```

1. Example that defines the `onOpen`, `onMemberOpen`, and `onMessage` callbacks

   ```javascript
   jatos.joinGroup({
     "onOpen": onOpen,
     "onMemberOpen": onMemberOpen,
     "onMessage": onMessage
   });

   function onOpen() {
     alert("You joined a group and opened a group channel");
   }

   function onMemberOpen(memberId) {
     alert("In our group another member (ID " + memberId + ") opened a group channel");
   }

   function onMessage(msg) {
     alert("You received a message: " + msg);
   }
   ```


### `jatos.sendGroupMsg`

Sends a message to all group members with an open group channel. Use `jatos.sendGroupMsgTo` to send a message to a particular member.

Between group members data can be exchanged in fundamentally two different ways: sendGroupMsg/sendGroupMsgTo or the [Group Session](#functions-to-access-the-group-session). The main difference is that the Group Session is stored in JATOS database on the server side while with sendGroupMsg/sendGroupMsgTo the data are only relayed on the server side but is never stored. E.g. if the worker reloads the page all prior messages sent by sendGroupMsg/sendGroupMsgTo will be lost - on the other side, everything stored in the Group Session will be restored. But this storage of the Group Session in JATOS comes at the cost of being (slightly) slower. Which option to choose depends mostly on your study design. If you expect your workers to have an unreliable Internet connection or to reload the page then you should use the Group Session. If you just want to 'stream' current data to other members the use sendGroupMsg/sendGroupMsgTo.

* _@param {object} msg_ - Any JavaScript object

**Example**

   ```javascript
   var msg = "Message for every group member"; // Send a text message
   jatos.sendGroupMsg(msg)

   var objMsg = {"city": "Berlin", "population": 3500000}; // Send an object
   jatos.sendGroupMsg(objMsg)
   ```


### `jatos.sendGroupMsgTo`

Like `jatos.sendGroupMsg` but sends a message to a particular group member specified by the group member ID. You can find a list of all IDs of group members with an open channel `jatos.groupChannels`. Alternativally you get member IDs via the `onMemberOpen` callback function.

* _@param {string} recipient_ - Recipient's group member ID
* _@param {object} msg_ - Any JavaScript object

**Examples**

1. Send a message to a group member with ID 1063

   ```javascript
   var msg = "Message for group member 1063";
   jatos.sendGroupMsgTo("1063", msg)
   ```

1. Use the `onMemberOpen` callback to send a message right after a new member opened their group channel

   ```javascript
   jatos.joinGroup({
     "onMemberOpen": onMemberOpen,
     "onMessage": onMessage
   });

   function onMemberOpen(memberId) {
     var msg = "Welcome to the group!";
     jatos.sendGroupMsgTo(memberId, msg);
   }

   function onMessage(msg) {
      alert("You received a message: " + msg);
   }
   ```


### `jatos.leaveGroup`

Leaves the group it has previously joined. It offers callbacks, either as parameter or via [jQuery.deferred.promise](https://api.jquery.com/deferred.promise/), to signal success or failure in the leaving.

* _@param {optional function} onSuccess_ - Function to be called after the group is left
* _@param {optional function} onError_ - Function to be called in case of error
* _@return {jQuery.deferred.promise}_

**Example**

```javascript
jatos.leaveGroup();
```


### `jatos.reassignGroup`

Asks the JATOS server to reassign this study run to a different group. JATOS can only reassign if there is another group availible. It offers callbacks, either as parameter or via [jQuery.deferred.promise](https://api.jquery.com/deferred.promise/), to signal success or failure in the reassigning.

* _@param {optional function} onSuccess_ - Function to be called if the reassignment was successful
* _@param {optional function} onFail_ - Function to be called if the reassignment was unsuccessful
* _@return {jQuery.deferred.promise}_

**Example**

```javascript
var deferred = jatos.reassignGroup();
deferred.done(() => { alert("Successful group reassignment: new group ID is " + jatos.groupResultId) });
deferred.fail(() => { alert("Group reassignment failed") });
```


### `jatos.setGroupFixed`

Ask the JATOS server to fix this group. A fixed group is not allowed to take on more members although members are still allowed to leave. It offers callbacks, either as parameter or via [jQuery.deferred.promise](https://api.jquery.com/deferred.promise/), to signal success or failure in the fixing.

* _@param {optional function} onSuccess_ - Function to be called if the fixing was successful
* _@param {optional function} onFail_ - Function to be called if the fixing was unsuccessful
* _@return {jQuery.deferred.promise}_

**Example**

```javascript
jatos.setGroupFixed();
```


### `jatos.hasJoinedGroup`

Returns true if this study run joined a group and false otherwise. It doesn't necessarily mean that we have an open group channel. We might just have joined a group in a prior component but in this component never opened the channel. If you want to check for an open group channel use `jatos.hasOpenGroupChannel`.

**Example**

```javascript
if(jatos.hasJoinedGroup()) {
  // We are member in a group
} else {
  // We are not member in a group
};
```


### `jatos.hasOpenGroupChannel`

Returns true if we currently have an open group channel and false otherwise. Since you can't open a group channel without joining a group, it also means that we joined a group. On the other side although we have closed group channel we can still be a member in a group. Use `jatos.hasJoinedGroup` to check group membership.

**Example**

```javascript
if(jatos.hasOpenGroupChannel()) {
  // We are member in a group and have an open group channel
} else {
  // We do not have an open group channel (but could still be member in a group)
};
```


### `jatos.isMaxActiveMemberReached`

Returns true if the group has reached the maximum amount of active members like specified in the batch properties. It's not necessary that each member has an open group channel.

**Example**

```javascript
if(jatos.isMaxActiveMemberReached()) {
  // Maximum number of active members is reached
};
```


### `jatos.isMaxActiveMemberOpen`

Returns true if the group has reached the maximum amount of active members like specified in the batch properties and each member has an open group channel.

**Example**

```javascript
if(jatos.isMaxActiveMemberOpen()) {
  // Maximum number of active members is reached and each has an open channel
};
```


### `jatos.isGroupOpen`

Returns true if all active members of the group have an open group channel and can send and receive data. It's not necessary that the group has reached its minimum or maximum active member size.

**Example**

```javascript
if(jatos.isGroupOpen()) {
  // Each of the current members of the group have an open group channel
};
```


## Functions to access the Group Session

The Group Session is one of three way to communicate between members of a group. The others are direct messaging (with [jatos.sendGroupMsgTo](#jatossendgroupmsgtorecipient-msg)) and broadcast messaging ([jatos.sendGroupMsg](#jatossendgroupmsgmsg)) (or: [more general information about the different session types](/Session-Data-Three-Types.html)).

In difference to the [Batch Session](#functions-to-access-the-batch-session) the Group Session doesn't work from the start of a component. To use the Group Session you have to join a group ([with jatos.joinGroup](#jatosjoingroupcallbacks)). There you can also define a `onGroupSession` callback that gets called each time the Group Session changes regardless of the origin of the change.

The Group Session is stored in JATOS' database on the server side. That means that all changes in the Group Session have to be synchronized between the client and the server. This is done via the group channel. Therefore all writing functions (`add`, `remove`, `clear`, `replace`, `copy`, `move`, `set`, `setAll`) can be paired with callback functions that will signal  success or failure in the client-server sync. These callback functions can be either passed as parameters to `jatos.groupSession.[function_name]` or via [jQuery.deferred.promise](https://api.jquery.com/deferred.promise/).

On the other side for all reading functions (`get`, `find`, `getAll`, `test`) there is no need to sync data between client and server, because jatos.js keeps a copy of the Group Session locally. Therefore all reading functions do not offer callbacks, because there is no risk of failure of synchronization.

Accessing the Group Session is done via [JSON Patches (RFC 6902)](https://tools.ietf.org/html/rfc6902) and 
[JSON Pointer (RFC 6901)](https://tools.ietf.org/html/rfc6901). An introduction can be found under [jsonpatch.com](http://jsonpatch.com/). For JSON Patches jatos.js uses the [JSON-Patch](https://github.com/Starcounter-Jack/JSON-Patch) library from Joachim Wester and for JSON Pointers the [jsonpointer.js](https://github.com/alexeykuzmin/jsonpointer.js) library from Alexey Kuzmin.


### `jatos.groupSession.add`

JSON Patch add operation: Adds a value to an object or inserts it into an array. In the case of an array, the value is inserted before the given index. The `-` character can be used instead of an index to insert at the end of an array (see [jsonpatch.com](http://jsonpatch.com/)). If the path already exists in the Group Session the value will be overwritten.

* _@param {string} path_ - JSON pointer path 
* _@param {object} value_ - value to be stored
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

**Examples**

1. Add an a field to the Group Session 

   If the Group Session is `{"a": 100}` and one calls

   ```javascript
   jatos.groupSession.add("/b", 123);
   ```

   then after the Group Session is successfully updated the new object is `{"a": 100, "b": 123}`.

   Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

1. Catch failures with jQuery's defered

   ```javascript
   var deferred = jatos.groupSession.add("/b", 123);
   deferred.done(() => { alert("Group Session was successfully updated") });
   deferred.fail(() => { alert("Group Session synchronization failed") });
   ```

1. Example with an array: Put the object `{id: 123, name: "Max"}` after the second position of the array with the path `/subjects`:

   ```javascript
   var deferred = jatos.groupSession.add("/subjects/2", {id: 123, name: "Max"});
   deferred.done(() => { alert("Batch Session was successfully updated") });
   deferred.fail(() => { alert("Batch Session synchronization failed") });
   ```

1. Example of how to append to the end of an array: use `/-` after the arrays name:

   ```javascript
   var deferred = jatos.groupSession.add("/subjects/-", {id: 124, name: "Adam"});
   deferred.done(() => { alert("Batch Session was successfully updated") });
   deferred.fail(() => { alert("Batch Session synchronization failed") });
   ```


### `jatos.groupSession.remove`

JSON Patch remove operation: Removes a value from an object or array (see [jsonpatch.com](http://jsonpatch.com/)).

* _@param {string} path_ - JSON pointer path to the field that should be removed
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

**Examples**

1. Remove a field from the Group Session

   If the Group Session is `{"a": 100, "b": 123}` and one calls

   ```javascript
   jatos.groupSession.remove("/b");
   ```

   then after the Group Session is successfully updated the new object is `{"a": 100}`.

   Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

1. Catch failures with jQuery's defered

   ```javascript
   var deferred = jatos.groupSession.remove("/b");
   deferred.done(() => { alert("Group Session was successfully updated") });
   deferred.fail(() => { alert("Group Session synchronization failed") });
   ```


### `jatos.groupSession.replace`

JSON Patch replace operation: Replaces a value. Equivalent to a “remove” followed by an “add” (see [jsonpatch.com](http://jsonpatch.com/)).

* _@param {string} path_ - JSON pointer path 
* _@param {object} value_ - value to be replaced with
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

**Examples**

1. Replace a field in the Group Session

   If the Group Session is `{"a": 100, "b": 123}` and one calls

   ```javascript
   jatos.groupSession.replace("/b", 789);
   ```

   then after the Group Session is successfully updated the new object is `{"a": 100, "b": 789}`.

   Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

1. Catch failures with jQuery's defered

   ```javascript
   var deferred = jatos.groupSession.replace("/b", 789);
   deferred.done(() => { alert("Group Session was successfully updated") });
   deferred.fail(() => { alert("Group Session synchronization failed") });
   ```


### `jatos.groupSession.copy`

JSON Patch copy operation: Copies a value from one location to another within the JSON document. Both from and path are JSON Pointers (see [jsonpatch.com](http://jsonpatch.com/)).

* _@param {string} from_ - JSON pointer path to the origin 
* _@param {string} path_ - JSON pointer path to the target
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

**Examples**

1. Copy a field in the Group Session from one location to another

   If the Group Session is `{"a": "jatos"}` and one calls

   ```javascript
   jatos.groupSession.copy("/a", "/b");
   ```

   then after the Group Session is successfully updated the new object is `{"a": "jatos", "b": "jatos"}`.

   Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

1. Catch failures with jQuery's defered

   ```javascript
   var deferred = jatos.groupSession.copy("/a", "/b");
   deferred.done(() => { alert("Group Session was successfully updated") });
   deferred.fail(() => { alert("Group Session synchronization failed") });
   ```


### `jatos.groupSession.move`

JSON Patch move operation: Moves a value from one location to the other. Both from and path are JSON Pointers. (see [jsonpatch.com](http://jsonpatch.com/)).

* _@param {string} from_ - JSON pointer path to the origin 
* _@param {string} path_ - JSON pointer path to the target
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

**Examples**

1. Move a field in the Group Session from one location to another

   If the Group Session is `{"a": "jatos"}` and one calls

   ```javascript
   jatos.groupSession.move("/a", "/b");
   ```

   then after the Group Session is successfully updated the new object is `{"b": "jatos"}`.

   Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

1. Catch failures with jQuery's defered

   ```javascript
   var deferred = jatos.groupSession.move("/a", "/b");
   deferred.done(() => { alert("Group Session was successfully updated") });
   deferred.fail(() => { alert("Group Session synchronization failed") });
   ```


### `jatos.groupSession.find`

Gets a field in the Group Session data. Takes a JSON Pointer and returns the matching value. Gets the object from the locally stored copy of the session and does not call the server. Contrary to `jatos.groupSession.get` it allows to get values from all levels of the Group Session's object tree.

* _@param {string} path_ - JSON pointer path 
* _@return {object}_ - the value that is stored in path

**Example**

Given the Group Session is `{"a": {"a1": "foo", "a2": "bar"}, "b": 999}`

```javascript
jatos.groupSession.find("/a/a1"); // returns "foo"
jatos.groupSession.find("/b"); // returns 999
```

the first line returns "foo" and the second 999.


### `jatos.groupSession.defined`

**Since JATOS version >= 3.1.8** - Checks in the Group Session whether a field under the given path exists. Returns true if the field is defined and false otherwise. It's equivalent to `!jatos.groupSession.test(path, undefined)`.

* _@param {string} path_ - JSON pointer path to be checked
* _@return {boolean}_

**Example**

```javascript
jatos.groupSession.defined("/a"); // returns true if the pointer '/a' exists
```


### `jatos.groupSession.test`

JSON Patch test operation: Tests that the specified value is set in the document (see [jsonpatch.com](http://jsonpatch.com/)).

* _@param {string} path_ - JSON pointer path to be tested
* _@param {object} value_ - value to be tested
* _@return {boolean}_

**Example**

Given the Group Session is `{"a": 123, "b": {"b1": "flowers", "b2": "animals"}}`

```javascript
jatos.groupSession.test("/a", 123); // returns true
jatos.groupSession.test("/a", 10); // returns false
jatos.groupSession.test("/b/b1", "flowers"); // returns true
```

the first line returns true, second false and third true.


### `jatos.groupSession.get`

Convenience function: like `jatos.groupSession.find` but works with a key instead of a JSON Pointer (without the slash in front of the key name). Therefore it works only on the first level of the session's object tree. It takes a name of an field within the Group Session and returns the matching value.  For all other levels of the object tree use jatos.groupSession.find. Gets the object from the locally stored copy of the session and does not call the server.

* _@param {string} name_ - name of the field 
* _@return {object}_ - the value that is stored under name

**Examples**

1. Get a field from the Group Session

   Given the Group Session is `{"a": 1000, "b": "watermelon"}`

   ```javascript
   // Since the parameter is the key's name and not a path it does not start with a "/"
   var b = jatos.groupSession.get("b"); // b is "watermelon"
   var c = jatos.groupSession.get("c"); // c is undefined
   ```

   the first line returns "watermelon" and the second undefined.

1. With `jatos.groupSession.get` you can only access the first level of the object tree - if you want another level use `jatos.groupSession.find`.

   If the Group Session is `{"a": {"a1": 123, "a2": "watermelon"}}`

   ```javascript
   var a1 = jatos.groupSession.get("a1"); // a1 is undefined !!!
   var a = jatos.groupSession.get("a"); // a is { "a1": 123, "a2": "watermelon" }
   ```


### `jatos.groupSession.set`

A convenience function for `jatos.groupSession.add`. Instead of a JSON Pointer path it accepts a name of the field to be stored (without the slash in front). Therefore it works only on the first level of the Group Session's object tree. If the name already exists in the Group Session the value will be overwritten.

* _@param {string} name_ - name of the field 
* _@param {object} value_ - value to be stored
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

**Examples**

1. Set a field in the Group Session

   If the Group Session is `{"a": 1234}`

   ```javascript
   // Since the parameter is the key's name and not a path it does not start with a "/"
   var b = jatos.groupSession.set("b", "koala");
   ```

   then after the Group Session is successfully updated the new object is `{"a": 1234, "b": "koala"}`.

   Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

1. Catch failures with jQuery's defered

   ```javascript
   var deferred = jatos.groupSession.set("b", "koala");
   deferred.done(() => { alert("Group Session was successfully updated") });
   deferred.fail(() => { alert("Group Session synchronization failed") });
   ```


### `jatos.groupSession.getAll`

Returns the complete Group Session data (might be bad performance-wise). Gets the object from the locally stored copy of the session and does not call the server.

* _@return {object}_ Returns the whole Group Session object

**Example**

```javascript
var groupSession = jatos.groupSession.getAll();
```


### `jatos.groupSession.setAll`

Replaces the whole session data. If the replacing object is rather large it might be better performance-wise to replace only individual paths. Each session writting involves sending the changes in the session via a JSON Patch to the JATOS server. If the session is large this data transfer can take some time. In this case use other session functions, like 'set', 'add', or 'replace'.

* _@param {object} value_ - value to be stored in the session
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

**Examples**

1. Set the whole Group Session at once

   ```javascript
   var o = {"a": 123, "b": "foo"};
   jatos.groupSession.setAll(o); // Overwrites the current Group Session with the object o
   ```

   Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

1. Catch failures with jQuery's defered

   ```javascript
   var o = {"a": 123, "b": "foo"};
   var deferred = jatos.groupSession.setAll(o);
   deferred.done(() => { alert("Group Session was successfully updated") });
   deferred.fail(() => { alert("Group Session synchronization failed") });
   ```


### `jatos.groupSession.clear`

Clears the whole Group Session data and sets it to an empty object `{}`.

* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

**Examples**

1. Clear the whole Group Session

   ```javascript
   jatos.groupSession.clear();
   ```

   Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

1. Catch failures with jQuery's defered

   ```javascript
   var deferred = jatos.groupSession.clear();
   deferred.done(() => { alert("Group Session was successfully updated") });
   deferred.fail(() => { alert("Group Session synchronization failed") });
   ```
