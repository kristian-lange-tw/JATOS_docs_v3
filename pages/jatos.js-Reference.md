---
title: jatos.js Reference
keywords: reference, jatos.js
tags:
summary: jatos.js is a small JavaScript library that helps you to communicate from your component's JavaScript with your JATOS server. Below we list and describe the variables and functions of the jatos.js library.
sidebar: mydoc_sidebar
permalink: jatos.js-Reference.html
folder:
toc: true
last_updated: 4 July 2017
---

Have a look at what's [mandatory in HTML and JavaScript for JATOS components](Mandatory-lines-in-your-components-HTML.html). Always load the jatos.js script in the `<head>` section with the following line:

```
<script src="/assets/javascripts/jatos.js"></script>
```

All variables or calls to jatos.js start with `jatos.`. For example, if you want to get the study's ID you use `jatos.studyId`. If you submit result data of your component back to your JATOS server you use `jatos.submitResultData(resultData)`, where resultData can be any kind of text.

And, please, if you find a mistake or have a question don't hesitate to [contact us](Contact-us.html).


## jatos.js variables

You can call any of these variables below at any point in your HTML file after jatos.js finished initializing (`jatos.onload()` will be called). Most variables are read-only. A few variables can be written into (e.g. `jatos.httpTimeout`). Those are marked '(writeable)'.

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
* `jatos.groupState` - Represents the state of the group in JATOS; only set if group channel is open (one of STARTED, FIXED, FINISHED)
* `jatos.groupMembers` - List of member IDs of the current members of the group
* `jatos.groupChannels` - List of member IDs of the currently open group channels


### ~~Group's session data~~

**Removed** - As of JATOS v3 the Group Session data can be accessed via the [`jatos.groupSession` functions](#functions-to-access-the-group-session).

~~* `jatos.groupSessionData` - Group Session data shared in between members of the group (see also [Session Data - Three Types](Session-Data-Three-Types.html))~~


### Other variables

* `jatos.version` - Current version of the jatos.js library
* `jatos.channelSendingTimeoutTime` (writeable) - Time in ms to wait for an answer after sending a message via a channel (batch or group). Set this variable if you want to change the default value (default is 10 s).

  ```javascript
  jatos.channelSendingTimeoutTime = 20000; // Sets channel timeout to 20 seconds
  ```

* `jatos.httpTimeout` (writeable) - Time in ms to wait for an answer of an HTTP request by jatos.js. Set this variable if you want to change the default value (default is 1 min).

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

* `jatos.jQuery` - You can always use jatos.js own jQuery if you want to save some bandwidth

## General jatos.js functions

### `jatos.onLoad(callback)`

Defines callback function that jatos.js will call when it's finished initialising. Only [mandatory](Mandatory-lines-in-your-components-HTML.html) call in every component.

* @param {Function} callback - function to be called after jatos.js' initialization is done

Example:

```javascript
jatos.onLoad(function() {
  // Start here with your code that uses jatos.js' variables and functions
});
```

### `jatos.onError(callback)`

Defines a callback function that is to be called in case jatos.js produces an error. 

* @param {Function} callback - Function to be called in case of an error

Example that shows the error message in an alert box:

```javascript
jatos.onError(function(error) {
  alert(error);
});
```

### `jatos.log(logMsg)`

Sends a message to be logged back to the JATOS server where it will be logged in JATOS' log file.

* _@param {String} logMsg_ - The messages to be logged  

Example:

```javascript
jatos.log("Log this message in JATOS' log file");
```

### `jatos.addJatosIds(obj)`

Convenience function that adds some [IDs](jatos.js-Reference.html#ids) (study ID, study title, batch ID, batch title, component ID, component position, component title, worker ID, study result ID, component result ID, group result ID, group member ID) to the given object.

* _@param {Object} obj_ - Object to which the IDs will be added

Example:

```javascript
var resultData = {};
jatos.addJatosIds(resultData);
```

### `jatos.setHeartbeatPeriod(heartbeatPeriod)`

Every running component sends regularly a HTTP request (the heartbeat) back to the JATOS server. This signals that it is still running. As soon as the browser tab running the component is closed the heartbeat ceases. The time of the last heartbeat is visible in the GUI, in the study results page in the 'Last Seen' row. This way you can easily see if a worker is still running your study or if (and when) he abandonend it. By default the heartbeat period is 2 minutes. By careful not to set the period too low (few seconds or even milliseconds) since it might overload your network or your JATOS server.

* _@param {Number} heartbeatPeriod_ - Time period between two heartbeats in milliseconds

Example:

```javascript
jatos.setHeartbeatPeriod(60000); // Sets to a heartbeat every minute
```

## Functions to control study flow

### `jatos.startComponent(componentId)`

Finishes the currently running component and starts the component with the given ID.

* _@param {Number} componentId_ - ID of the component to start

Example:

```javascript
jatos.startComponent(23); // Jumps to component with ID 23
```

### `jatos.startComponentByPos(componentPos)`

Finishes the currently running component and starts the component with the given position. The component position is the count of the component within the study like shown in the study overview page (1st component has position 1, 2nd component position 2, ...).

* _@param {Number} componentPos_ - Position of the component to start

Example:

```javascript
jatos.startComponentByPos(3); // Jumps to component with position 3
```

### `jatos.startNextComponent()`

Finishes the currently running component and starts the next component of this study. The next component is the one with position + 1. The component position is the count of the component within the study like shown in the study overview page (1st component has position 1, 2nd component position 2, ...).

Example:

```javascript
jatos.startNextComponent(); // Jumps to the next component
```

It's often used together with `jatos.submitResultData` to first submit result data back to the JATOS server and afterwards jump to the next component:

```javascript
var resultData = "my important result data";
jatos.submitResultData(resultData, jatos.startNextComponent);
```

### `jatos.startLastComponent()`

Finishes the current component and starts the last component of this study. If the last component is inactive it starts the component with the highest position that is active. The component position is the count of the component within the study like shown in the study overview page (1st component has position 1, 2nd component position 2, ...).

Example:

```javascript
jatos.startLastComponent(); // Jumps to the last component
```

### `jatos.endComponent(successful, errorMsg, onSuccess, onError)`

**Deprecated**: Will be removed in future versions. Use `jatos.startComponent`, `jatos.startComponentByPos`, `jatos.startNextComponent`, or `jatos.startLastComponent` instead.

Finishes component. Usually this is not necessary because the last component is automatically finished if the new component is started. Nevertheless it's useful to explicitly tell about a FAIL and submit an error message. Finishing the component doesn't finish the study.

* _@param {optional Boolean} successful_ - 'true' if study should finish successful and the participant should get the confirmation code - 'false' otherwise.
* _@param {optional String} errorMsg_ - Error message that should be logged.
* _@param {optional Function} onSuccess_ - Function to be called in case of successful submit
* _@param {optional Function} onError_ - Function to be called in case of error

### `jatos.abortStudyAjax(message, success, error)`

Aborts study via an Ajax call - afterwards the study is not redirected to the JATOS' end page. All previously submitted result data will be deleted. It offers callbacks, either as parameter or via [jQuery.deferred.promise](https://api.jquery.com/deferred.promise/), to signal success or failure in the aborting.

* _@param {optional String} message_ - Message that should be logged
* _@param {optional Function} success_ - Function to be called in case of successful submit
* _@param {optional Function} error_ - Function to be called in case of error
* _@return {jQuery.deferred.promise}_

Example:

```javascript
jatos.abortStudyAjax("Aborted study: user pressed abort button");
```

### `jatos.abortStudy(message)`

Aborts study. All previously submitted result data will be deleted. Afterwards the worker is redirected to the study end page.

* _@param {optional String} message_ - Message that should be logged

Example:

```javascript
jatos.abortStudy("Aborted study: user pressed abort button");
```

### `jatos.endStudyAjax(successful, errorMsg, onSuccess, onError)`

Ends study with an Ajax call - afterwards the study is not redirected to the JATOS' end page. It offers callbacks, either as parameter or via [jQuery.deferred.promise](https://api.jquery.com/deferred.promise/), to signal success or failure in the ending.

* _@param {optional Boolean} successful_ - 'true' if study should finish successful and the participant should get the confirmation code - 'false' otherwise.
* _@param {optional String} errorMsg_ - Error message that should be logged.
* _@param {optional Function} onSuccess_ - Function to be called in case of successful submit
* _@param {optional Function} onError_ - Function to be called in case of error
* _@return {jQuery.deferred.promise}_

Example:

```javascript
jatos.endStudyAjax(false, "internal JS error");
```

### `jatos.endStudy(successful, errorMsg)`

Ends study. Redirects the worker to the study end page afterwards.

* _@param {optional Boolean} successful_ - 'true' if study should finish successfully, 'false' otherwise. Default is true.
* _@param {optional String} errorMsg_ - Error message that should be logged.

Example:

```javascript
jatos.endStudy();
```

## Functions for Study Session and result data

### `jatos.submitResultData(resultData, onSuccess, onError)`

Posts result data for the currently running component back to the JATOS server. Already stored result data for this component will be **overwritten**. If you want to append result data use `jatos.appendResultData` instead. It offers callbacks, either as parameter or via [jQuery.deferred.promise](https://api.jquery.com/deferred.promise/), to signal success or failure in the transfer.

* _@param {String} resultData_ - String to be submitted
* _@param {optional Function} success_ - Function to be called in case of successful submit
* _@param {optional Function} error_ - Function to be called in case of error
* _@return {jQuery.deferred.promise}_

Example:

```javascript
var resultData = { "a": 123, "b": 789, "c": 100};
jatos.submitResultData(JSON.stringify(resultData));
```

It's often used together with `jatos.startNextComponent` to first submit result data back to the JATOS server and afterwards jump to the next component:

```javascript
var resultData = { "a": 123, "b": 789, "c": 100};
jatos.submitResultData(JSON.stringify(resultData), jatos.startNextComponent);
```

### `jatos.appendResultData(resultData, onSuccess, onError)`

**Since JATOS version >= 3.1.7**

Appends result data to the already posted result data. Contrary to jatos.submitResultData it does not overwrite the result data. It offers callbacks, either as parameter or via [jQuery.deferred.promise](https://api.jquery.com/deferred.promise/), to signal success or failure in the transfer. This function can be used several times during an component run to incrementally save result data.

* _@param {String} resultData_ - String to be appended
* _@param {optional Function} success_ - Function to be called in case of successful submit
* _@param {optional Function} error_ - Function to be called in case of error
* _@return {jQuery.deferred.promise}_

Example:

```javascript
var resultData = { "a": 123, "b": 789, "c": 100};
jatos.appendResultData(JSON.stringify(resultData));
```

### `jatos.setStudySessionData(studySessionData, onSuccess, onFail)`

Posts Study Session data to the JATOS server. This function is called automatically in the end of a component's life cycle (it's called by all jatos.js functions that end a component). So unless you want to store the session data in between a component run it's not necessary to call this function manually. It offers callbacks, either as parameter or via [jQuery.deferred.promise](https://api.jquery.com/deferred.promise/), to signal success or failure in the transfer.

* _@param {Object} sessionData_ - Object to be submitted
* _@param {optional Function} onSuccess_ - Function to be called after this function is finished
* _@param {optional Function} onFail_ - Function to be called after if this this functions fails
* _@return {jQuery.deferred.promise}_

Example:

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


### `jatos.batchSession.add(path, value, onSuccess, onFail)`

JSON Patch add operation: Adds a value to an object or inserts it into an array. In the case of an array, the value is inserted before the given index. The `-` character can be used instead of an index to insert at the end of an array (see [jsonpatch.com](http://jsonpatch.com/)). If the path already exists in the Batch Session the value will be overwritten.

* _@param {string} path_ - JSON pointer path 
* _@param {object} value_ - value to be stored
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

Example: If the internal Batch Session is `{"a": 100}` and one calls

```javascript
jatos.batchSession.add("/b", 123);
```
then after the Batch Session is successfully updated the new internal object is `{"a": 100, "b": 123}`.

Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

Example with jQuery's defered:

```javascript
var deferred = jatos.batchSession.add("/b", 123);
deferred.done(function () {
  alert("Batch Session was successfully updated");
});
deferred.fail(function () {
  alert("Batch Session synchronization failed");
});
```


### `jatos.batchSession.remove(path, onSuccess, onFail)`

JSON Patch remove operation: Removes a value from an object or array (see [jsonpatch.com](http://jsonpatch.com/)).

* _@param {string} path_ - JSON pointer path to the field that should be removed
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

Example: If the internal Batch Session is `{"a": 100, "b": 123}` and one calls

```javascript
jatos.batchSession.remove("/b");
```

then after the Batch Session is successfully updated the new internal object is `{"a": 100}`.

Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

Example with jQuery's defered:

```javascript
var deferred = jatos.batchSession.remove("/b");
deferred.done(function () {
  alert("Batch Session was successfully updated");
});
deferred.fail(function () {
  alert("Batch Session synchronization failed");
});
```

### `jatos.batchSession.replace(path, value, onSuccess, onFail)`

JSON Patch replace operation: Replaces a value. Equivalent to a 'remove' followed by an 'add' (see [jsonpatch.com](http://jsonpatch.com/)).

* _@param {string} path_ - JSON pointer path 
* _@param {object} value_ - value to be replaced with
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

Example: If the internal Batch Session is `{"a": 100, "b": 123}` and one calls

```javascript
jatos.batchSession.replace("/b", 789);
```

then after the Batch Session is successfully updated the new internal object is `{"a": 100, "b": 789}`.

Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

Example with jQuery's defered:

```javascript
var deferred = jatos.batchSession.replace("/b", 789);
deferred.done(function () {
  alert("Batch Session was successfully updated");
});
deferred.fail(function () {
  alert("Batch Session synchronization failed");
});
```

### `jatos.batchSession.copy(from, path, onSuccess, onFail)`

JSON Patch copy operation: Copies a value from one location to another within the JSON document. Both from and path are JSON Pointers (see [jsonpatch.com](http://jsonpatch.com/)).

* _@param {string} from_ - JSON pointer path to the origin 
* _@param {string} path_ - JSON pointer path to the target
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

Example: If the internal Batch Session is `{"a": "jatos"}` and one calls

```javascript
jatos.batchSession.copy("/a", "/b");
```

then after the Batch Session is successfully updated the new internal object is `{"a": "jatos", "b": "jatos"}`.

Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

Example with jQuery's defered:

```javascript
var deferred = jatos.batchSession.copy("/a", "/b");
deferred.done(function () {
  alert("Batch Session was successfully updated");
});
deferred.fail(function () {
  alert("Batch Session synchronization failed");
});
```

### `jatos.batchSession.move(from, path, onSuccess, onFail)`

JSON Patch move operation: Moves a value from one location to the other. Both from and path are JSON Pointers. (see [jsonpatch.com](http://jsonpatch.com/)).

* _@param {string} from_ - JSON pointer path to the origin 
* _@param {string} path_ - JSON pointer path to the target
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

Example: If the internal Batch Session is `{"a": "jatos"}` and one calls

```javascript
jatos.batchSession.move("/a", "/b");
```

then after the Batch Session is successfully updated the new internal object is `{"b": "jatos"}`.

Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

Example with jQuery's defered:

```javascript
var deferred = jatos.batchSession.move("/a", "/b");
deferred.done(function () {
  alert("Batch Session was successfully updated");
});
deferred.fail(function () {
  alert("Batch Session synchronization failed");
});
```

### `jatos.batchSession.find(path)`

Gets a field in the Batch Session data. Takes a JSON Pointer and returns the matching value. Gets the object from the locally stored copy of the session and does not call the server. Contrary to `jatos.batchSession.get` it allows to get values from all levels of the Batch Session's object tree.

* _@param {string} path_ - JSON pointer path 
* _@return {object}_ - the value that is stored in path

Example: If the internal Batch Session is `{"a": {"a1": "foo", "a2": "bar"}, "b": 999}`

```javascript
jatos.batchSession.find("/a/a1"); // returns "foo"
jatos.batchSession.find("/b"); // returns 999
```

### `jatos.batchSession.defined(path)`

**Since JATOS version >= 3.1.8**

Checks in the Batch Session whether a field under the given path exists. Returns true if the field is defined and false otherwise. It's equivalent to `!jatos.batchSession.test(path, undefined)`.

* _@param {string} path_ - JSON pointer path to be checked
* _@return {boolean}_

Example:

```javascript
jatos.batchSession.defined("/a"); // returns true if the pointer '/a' exists
```

### `jatos.batchSession.test(path, value)`

JSON Patch test operation: Tests that the specified value is set in the document (see [jsonpatch.com](http://jsonpatch.com/)).

* _@param {string} path_ - JSON pointer path to be tested
* _@param {object} value_ - value to be tested
* _@return {boolean}_

Example: If the internal Batch Session is `{"a": 123, "b": {"b1": "flowers", "b2": "animals"}}`

```javascript
jatos.batchSession.test("/a", 123); // returns true
jatos.batchSession.test("/a", 10); // returns false
jatos.batchSession.test("/b/b1", "flowers"); // returns true
```

Example: If you want to know the existence of a path in the Batch Session you can test against `undefined`:

```javascript
if (!jatos.batchSession.test("/c", undefined)) {
  // Path "/c" exists
} else {
  // Path "/c" doesn't exist
}
```

### `jatos.batchSession.get(name)`

Convenience function: like `jatos.batchSession.find` but works with a key instead of a JSON Pointer. Therefore it works only on the first level of the session's object tree. It takes a name of an field within the Batch Session and returns the matching value.  For all other levels of the object tree use jatos.batchSession.find. Gets the object from the locally stored copy of the session and does not call the server.

* _@param {string} name_ - name of the field 
* _@return {object}_ - the value that is stored under name

Example: If the internal Batch Session is `{"a": 1000, "b": "watermelon"}`

```javascript
// Since the parameter is the key's name and not a path it does not start with a "/"
var b = jatos.batchSession.get("b"); // b is "watermelon"
var c = jatos.batchSession.get("c"); // c is undefined
```

Example: With `jatos.batchSession.get` you can only access the first level of the object tree - if you want another level use `jatos.batchSession.find`. If the internal Batch Session is `{"a": {"a1": 123, "a2": "watermelon"}}`

```javascript
var a1 = jatos.batchSession.get("a1"); // a1 is undefined !!!
var a = jatos.batchSession.get("a"); // a is { "a1": 123, "a2": "watermelon" }
```

### `jatos.batchSession.set(name, value, onSuccess, onFail)`

Like `jatos.batchSession.add`, but instead of a JSON Pointer path it accepts a name of the field to be stored. Therefore it works only on the first level of the Batch Session's object tree. If the name already exists in the Batch Session the value will be overwritten.

* _@param {string} name_ - name of the field 
* _@param {object} value_ - value to be stored
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

Example: If the internal Batch Session is `{"a": 1234}`

```javascript
// Since the parameter is the key's name and not a path it does not start with a "/"
var b = jatos.batchSession.set("b", "koala");
```

then after the Batch Session is successfully updated the new internal object is `{"a": 1234, "b": "koala"}`.

Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

Example with jQuery's defered:

```javascript
var deferred = jatos.batchSession.set("b", "koala");
deferred.done(function () {
  alert("Batch Session was successfully updated");
});
deferred.fail(function () {
  alert("Batch Session synchronization failed");
});
```

### `jatos.batchSession.getAll()`

Returns the complete Batch Session data. Gets the object from the locally stored copy of the session and does not call the server.

* _@return {object}_

Example:

```javascript
var batchSession = jatos.batchSession.getAll();
```

### `jatos.batchSession.setAll(value, onSuccess, onFail)`

Replaces the whole session data. If the replacing object is rather large it might be better performance-wise to replace only individual paths. Each session writting involves sending the changes in the session via a JSON Patch to the JATOS server. If the session is large this data transfer can take some time. In this case use other session functions, like 'set', 'add', or 'replace'.

* _@param {object} value_ - value to be stored in the session
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

Example:

```javascript
var o = {"a": 123, "b": "foo"};
jatos.batchSession.setAll(o); // Overwrites the current Batch Session with the object o
```

Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

Example with jQuery's defered:

```javascript
var o = {"a": 123, "b": "foo"};
var deferred = jatos.batchSession.setAll(o);
deferred.done(function () {
  alert("Batch Session was successfully updated");
});
deferred.fail(function () {
  alert("Batch Session synchronization failed");
});
```

### `jatos.batchSession.clear(onSuccess, onFail)`

Clears the whole Batch Session data and sets it to an empty object `{}`.

* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

Example:

```javascript
jatos.batchSession.clear();
```

Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

Example with jQuery's defered:

```javascript
var deferred = jatos.batchSession.clear();
deferred.done(function () {
  alert("Batch Session was successfully updated");
});
deferred.fail(function () {
  alert("Batch Session synchronization failed");
});
```

### `jatos.onBatchSession(callback)`

Defines a callback function that is called every time the Batch Session changes on the JATOS server side (that includes updates in the session originating from other workers that run the study in parallel).

* _@param {Function} path_ - Callback function that is called each time the Batch Session gets updated. The function has one parameter: the JSON pointer path to the changed field in the Batch Session.

Example:

```javascript
jatos.onBatchSession(function(path){
  alert("Batch Session was updated in path " + path);
});
```

Example: `onBatchSession` is often used together with `jatos.batchSession.find` to get the updated value:

```javascript
jatos.onBatchSession(function(path){
  var o = jatos.batchSession.find(path);
  if (typeof o != 'undefined') {
    alert("Batch Session was updated in path " + path + " to " + JSON.stringify(o));
  } else {
    // If the object under path was removed (e.g. with jatos.batchSession.remove) it can't be retrieved anymore
    alert("Batch Session was updated in path " + path);
  }
});
```

## Functions for group studies

### `jatos.joinGroup(callbacks)`

Tries to join a group and if it succeeds opens the group channel (which is mostly a WebSocket). Only if the group channel is open one can exchange data with other group members. As the only parameter this function takes an object that consists of several optional callback functions that will be called by jatos.js when certain group events occur. It returns a [jQuery.deferred.promise](https://api.jquery.com/deferred.promise/), to signal success or failure in joining.

* _@param {Object} callbacks_ - Defining callback functions for group events. All callbacks are optional. These callbacks functions are:
  * `onOpen`: Is called when the group channel is successfully opened
  * `onClose`: Is be called when the group channel is closed
  * `onError`: Is called if an error during opening of the group channel's WebSocket occurs or if an error is received via the group channel (e.g. the Group Session data couldn't be updated). If this function is not defined jatos.js will try to call the global `onJatosError` function.
  * `onMessage(msg)`: Is called if a message from another group member is received. It gets the message as a parameter.
  * `onMemberJoin(memberId)`: Is called when another member (not the worker running this study) joined the group. It gets the group member ID as a parameter.
  * `onMemberOpen(memberId)`: Is called when another member (not the worker running this study) opened a group channel. It gets the group member ID as a parameter.
  * `onMemberLeave(memberId)`: Is called when another member (not the worker running his study) left the group. It gets the group member ID as a parameter.
  * `onMemberClose(memberId)`: Is called when another member (not the worker running this study) closed his group channel. It gets the group member ID as a parameter.
  * `onGroupSession(path)`: Is called every time the Group Session changes on the JATOS server side. It gets the JSON pointer path to the changed field in the Group Session as a parameter.
  * `onUpdate()`: Combines several other callbacks. It's called if one of the following is called: `onMemberJoin`, `onMemberOpen`, `onMemberLeave`, `onMemberClose`, or `onGroupSession`.
* _@return {jQuery.deferred.promise}_

Minimal example that joins a group and receives updates via the Group Session:

```javascript
jatos.joinGroup({
  "onGroupSession": onGroupSession
});

function onGroupSession(path) {
   var o = jatos.groupSession.find(path);
   alert("Group Session was updated in path " + path + " to " + JSON.stringify(o));
}
```

Example that defines the `onOpen`, `onMemberOpen`, and `onMessage` callbacks: 

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

### `jatos.sendGroupMsg(msg)`

Sends a message to all group members with an open group channel. Use `jatos.sendGroupMsgTo` to send a message to a particular member.

Between group members data can be exchanged in fundamentally two different ways: sendGroupMsg/sendGroupMsgTo or the [Group Session](#functions-to-access-the-group-session). The main difference is that the Group Session is stored in JATOS database on the server side while with sendGroupMsg/sendGroupMsgTo the data are only relayed on the server side but is never stored. E.g. if the worker reloads the page all prior messages sent by sendGroupMsg/sendGroupMsgTo will be lost - on the other side, everything stored in the Group Session will be restored. But this storage of the Group Session in JATOS comes at the cost of being (slightly) slower. Which option to choose depends mostly on your study design. If you expect your workers to have an unreliable Internet connection or to reload the page then you should use the Group Session. If you just want to 'stream' current data to other members the use sendGroupMsg/sendGroupMsgTo.

* _@param {Object} msg_ - Any JavaScript object

Examples:

```javascript
var msg = "Message for every group member"; // Send a text message
jatos.sendGroupMsg(msg)

var objMsg = {"city": "Berlin", "population": 3500000"}; // Send an object
jatos.sendGroupMsg(objMsg)
```

### `jatos.sendGroupMsgTo(recipient, msg)`

Like `jatos.sendGroupMsg` but sends a message to a particular group member specified by the group member ID. You can find a list of all IDs of group members with an open channel `jatos.groupChannels`. Alternativally you get member IDs via the `onMemberOpen` callback function.

* _@param {String} recipient_ - Recipient's group member ID
* _@param {Object} msg_ - Any JavaScript object

Example:

```javascript
var msg = "Message for group member 1063";
jatos.sendGroupMsgTo("1063", msg)
```

In the next example we use the `onMemberOpen` callback to send a message right after a new member opened their group channel:

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

### `jatos.leaveGroup(onSuccess, onError)`

Leaves the group it has previously joined. It offers callbacks, either as parameter or via [jQuery.deferred.promise](https://api.jquery.com/deferred.promise/), to signal success or failure in the leaving.

* _@param {optional Function} onSuccess_ - Function to be called after the group is left
* _@param {optional Function} onError_ - Function to be called in case of error
* _@return {jQuery.deferred.promise}_

Example:

```javascript
jatos.leaveGroup();
```

### `jatos.reassignGroup(onSuccess, onFail)`

Asks the JATOS server to reassign this study run to a different group. JATOS can only reassign if there is another group availible. It offers callbacks, either as parameter or via [jQuery.deferred.promise](https://api.jquery.com/deferred.promise/), to signal success or failure in the reassigning.

* _@param {optional Function} onSuccess_ - Function to be called if the reassignment was successful
* _@param {optional Function} onFail_ - Function to be called if the reassignment was unsuccessful
* _@return {jQuery.deferred.promise}_

Example:

```javascript
var deferred = jatos.reassignGroup();
deferred.done(function () {
  alert("Successful group reassignment: new group ID is " + jatos.groupResultId);
});
deferred.fail(function () {
  alert("Group reassignment failed");
});
```

### ~~`jatos.setGroupSessionData(groupSessionData, onError)`~~

**Removed** - As of JATOS v3 the Group Session data can be access via the [`jatos.groupSession` functions](#functions-to-access-the-group-session).

~~Sends the Group Session data via the group channel to the JATOS server where it's stored and broadcasted to all members of this group. It either takes an Object as parameter or uses `jatos.groupSessionData` if the groupSessionData isn't provided. jatos.js tries several times to upload the session data, but if there are many concurrent members updating at the same time it might fail. But jatos.js/JATOS guarantees that it either persists the updated session data or calls the `onError` callback. In this way it is more reliable but slower compared to `jatos.sendGroupMsg` or `jatos.sendGroupMsgTo`. Since the Group Session is stored in the JATOS server it can be retrieved after a page reload or Internet connection problem to continue at the point of the interruption.~~

* ~~_@param {optional Object} groupSessionData_ - An object in JSON; If it's not given take _jatos.groupSessionData_~~
* ~~_@param {optional Object} onError_ - Function to be called if this upload was unsuccessful~~

### `jatos.setGroupFixed()`

Ask the JATOS server to fix this group. A fixed group is not allowed to take on more members although members are still allowed to leave. It offers callbacks, either as parameter or via [jQuery.deferred.promise](https://api.jquery.com/deferred.promise/), to signal success or failure in the fixing.

* _@param {optional Function} onSuccess_ - Function to be called if the fixing was successful
* _@param {optional Function} onFail_ - Function to be called if the fixing was unsuccessful
* _@return {jQuery.deferred.promise}_

Example:

```javascript
jatos.setGroupFixed();
```

### `jatos.hasJoinedGroup()`

Returns true if this study run joined a group and false otherwise. It doesn't necessarily mean that we have an open group channel. We might just have joined a group in a prior component but in this component never opened the channel. If you want to check for an open group channel use `jatos.hasOpenGroupChannel`.

Example:

```javascript
if(jatos.hasJoinedGroup()) {
  // We are member in a group
} else {
  // We are not member in a group
};
```

### `jatos.hasOpenGroupChannel()`

Returns true if we currently have an open group channel and false otherwise. Since you can't open a group channel without joining a group, it also means that we joined a group. On the other side although we have closed group channel we can still be a member in a group. Use `jatos.hasJoinedGroup` to check group membership.

Example:

```javascript
if(jatos.hasOpenGroupChannel()) {
  // We are member in a group and have an open group channel
} else {
  // We do not have an open group channel (but could still be member in a group)
};
```

### `jatos.isMaxActiveMemberReached()`

Returns true if the group has reached the maximum amount of active members like specified in the batch properties. It's not necessary that each member has an open group channel.

Example:

```javascript
if(jatos.isMaxActiveMemberReached()) {
  // Maximum number of active members is reached
};
```

### `jatos.isMaxActiveMemberOpen()`

Returns true if the group has reached the maximum amount of active members like specified in the batch properties and each member has an open group channel.

```javascript
if(jatos.isMaxActiveMemberOpen()) {
  // Maximum number of active members is reached and each has an open channel
};
```

### `jatos.isGroupOpen()`

Returns true if all active members of the group have an open group channel and can send and receive data. It's not necessary that the group has reached its minimum or maximum active member size.

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

### `jatos.groupSession.add(path, value, onSuccess, onFail)`

JSON Patch add operation: Adds a value to an object or inserts it into an array. In the case of an array, the value is inserted before the given index. The `-` character can be used instead of an index to insert at the end of an array (see [jsonpatch.com](http://jsonpatch.com/)). If the path already exists in the Group Session the value will be overwritten.

* _@param {string} path_ - JSON pointer path 
* _@param {object} value_ - value to be stored
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

Example: If the internal Group Session is `{"a": 100}` and one calls

```javascript
jatos.groupSession.add("/b", 123);
```
then after the Group Session is successfully updated the new internal object is `{"a": 100, "b": 123}`.

Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

Example with jQuery's defered:

```javascript
var deferred = jatos.groupSession.add("/b", 123);
deferred.done(function () {
  alert("Group Session was successfully updated");
});
deferred.fail(function () {
  alert("Group Session synchronization failed");
});
```

### `jatos.groupSession.remove(path, onSuccess, onFail)`

JSON Patch remove operation: Removes a value from an object or array (see [jsonpatch.com](http://jsonpatch.com/)).

* _@param {string} path_ - JSON pointer path to the field that should be removed
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

Example: If the internal Group Session is `{"a": 100, "b": 123}` and one calls

```javascript
jatos.groupSession.remove("/b");
```

then after the Group Session is successfully updated the new internal object is `{"a": 100}`.

Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

Example with jQuery's defered:

```javascript
var deferred = jatos.groupSession.remove("/b");
deferred.done(function () {
  alert("Group Session was successfully updated");
});
deferred.fail(function () {
  alert("Group Session synchronization failed");
});
```

### `jatos.groupSession.replace(path, value, onSuccess, onFail)`

JSON Patch replace operation: Replaces a value. Equivalent to a “remove” followed by an “add” (see [jsonpatch.com](http://jsonpatch.com/)).

* _@param {string} path_ - JSON pointer path 
* _@param {object} value_ - value to be replaced with
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

Example: If the internal Group Session is `{"a": 100, "b": 123}` and one calls

```javascript
jatos.groupSession.replace("/b", 789);
```

then after the Group Session is successfully updated the new internal object is `{"a": 100, "b": 789}`.

Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

Example with jQuery's defered:

```javascript
var deferred = jatos.groupSession.replace("/b", 789);
deferred.done(function () {
  alert("Group Session was successfully updated");
});
deferred.fail(function () {
  alert("Group Session synchronization failed");
});
```

### `jatos.groupSession.copy(from, path, onSuccess, onFail)`

JSON Patch copy operation: Copies a value from one location to another within the JSON document. Both from and path are JSON Pointers (see [jsonpatch.com](http://jsonpatch.com/)).

* _@param {string} from_ - JSON pointer path to the origin 
* _@param {string} path_ - JSON pointer path to the target
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

Example: If the internal Group Session is `{"a": "jatos"}` and one calls

```javascript
jatos.groupSession.copy("/a", "/b");
```

then after the Group Session is successfully updated the new internal object is `{"a": "jatos", "b": "jatos"}`.

Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

Example with jQuery's defered:

```javascript
var deferred = jatos.groupSession.copy("/a", "/b");
deferred.done(function () {
  alert("Group Session was successfully updated");
});
deferred.fail(function () {
  alert("Group Session synchronization failed");
});
```

### `jatos.groupSession.move(from, path, onSuccess, onFail)`

JSON Patch move operation: Moves a value from one location to the other. Both from and path are JSON Pointers. (see [jsonpatch.com](http://jsonpatch.com/)).

* _@param {string} from_ - JSON pointer path to the origin 
* _@param {string} path_ - JSON pointer path to the target
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

Example: If the internal Group Session is `{"a": "jatos"}` and one calls

```javascript
jatos.groupSession.move("/a", "/b");
```

then after the Group Session is successfully updated the new internal object is `{"b": "jatos"}`.

Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

Example with jQuery's defered:

```javascript
var deferred = jatos.groupSession.move("/a", "/b");
deferred.done(function () {
  alert("Group Session was successfully updated");
});
deferred.fail(function () {
  alert("Group Session synchronization failed");
});
```

### `jatos.groupSession.find(path)`

Gets a field in the Group Session data. Takes a JSON Pointer and returns the matching value. Gets the object from the locally stored copy of the session and does not call the server. Contrary to `jatos.groupSession.get` it allows to get values from all levels of the Group Session's object tree.

* _@param {string} path_ - JSON pointer path 
* _@return {object}_ - the value that is stored in path

Example: If the internal Group Session is `{"a": {"a1": "foo", "a2": "bar"}, "b": 999}`

```javascript
jatos.groupSession.find("/a/a1"); // returns "foo"
jatos.groupSession.find("/b"); // returns 999
```

### `jatos.groupSession.defined(path)`

**Since JATOS version >= 3.1.8**

Checks in the Group Session whether a field under the given path exists. Returns true if the field is defined and false otherwise. It's equivalent to `!jatos.groupSession.test(path, undefined)`.

* _@param {string} path_ - JSON pointer path to be checked
* _@return {boolean}_

Example:

```javascript
jatos.groupSession.defined("/a"); // returns true if the pointer '/a' exists
```

### `jatos.groupSession.test(path, value)`

JSON Patch test operation: Tests that the specified value is set in the document (see [jsonpatch.com](http://jsonpatch.com/)).

* _@param {string} path_ - JSON pointer path to be tested
* _@param {object} value_ - value to be tested
* _@return {boolean}_

Example: If the internal Group Session is `{"a": 123, "b": {"b1": "flowers", "b2": "animals"}}`

```javascript
jatos.groupSession.test("/a", 123); // returns true
jatos.groupSession.test("/a", 10); // returns false
jatos.groupSession.test("/b/b1", "flowers"); // returns true
```

### `jatos.groupSession.get(name)`

Convenience function: like `jatos.groupSession.find` but works with a key instead of a JSON Pointer. Therefore it works only on the first level of the session's object tree. It takes a name of an field within the Group Session and returns the matching value.  For all other levels of the object tree use jatos.groupSession.find. Gets the object from the locally stored copy of the session and does not call the server.

* _@param {string} name_ - name of the field 
* _@return {object}_ - the value that is stored under name

Example: If the internal Group Session is `{"a": 1000, "b": "watermelon"}`

```javascript
// Since the parameter is the key's name and not a path it does not start with a "/"
var b = jatos.groupSession.get("b"); // b is "watermelon"
var c = jatos.groupSession.get("c"); // c is undefined
```

Example: With `jatos.groupSession.get` you can only access the first level of the object tree - if you want another level use `jatos.groupSession.find`. If the internal Group Session is `{"a": {"a1": 123, "a2": "watermelon"}}`

```javascript
var a1 = jatos.groupSession.get("a1"); // a1 is undefined !!!
var a = jatos.groupSession.get("a"); // a is { "a1": 123, "a2": "watermelon" }
```

### `jatos.groupSession.set(name, value, onSuccess, onFail)`

Like `jatos.groupSession.add`, but instead of a JSON Pointer path it accepts a name of the field to be stored. Therefore it works only on the first level of the Group Session's object tree. If the name already exists in the Group Session the value will be overwritten.

* _@param {string} name_ - name of the field 
* _@param {object} value_ - value to be stored
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

Example: If the internal Group Session is `{"a": 1234}`

```javascript
// Since the parameter is the key's name and not a path it does not start with a "/"
var b = jatos.groupSession.set("b", "koala");
```

then after the Group Session is successfully updated the new internal object is `{"a": 1234, "b": "koala"}`.

Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

Example with jQuery's defered:

```javascript
var deferred = jatos.groupSession.set("b", "koala");
deferred.done(function () {
  alert("Group Session was successfully updated");
});
deferred.fail(function () {
  alert("Group Session synchronization failed");
});
```

### `jatos.groupSession.getAll()`

Returns the complete Group Session data (might be bad performance-wise). Gets the object from the locally stored copy of the session and does not call the server.

* _@return {object}_

Example:

```javascript
var groupSession = jatos.groupSession.getAll();
```

### `jatos.groupSession.setAll(value, onSuccess, onFail)`

Replaces the whole session data. If the replacing object is rather large it might be better performance-wise to replace only individual paths. Each session writting involves sending the changes in the session via a JSON Patch to the JATOS server. If the session is large this data transfer can take some time. In this case use other session functions, like 'set', 'add', or 'replace'.

* _@param {object} value_ - value to be stored in the session
* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

Example:

```javascript
var o = {"a": 123, "b": "foo"};
jatos.groupSession.setAll(o); // Overwrites the current Group Session with the object o
```

Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

Example with jQuery's defered:

```javascript
var o = {"a": 123, "b": "foo"};
var deferred = jatos.groupSession.setAll(o);
deferred.done(function () {
  alert("Group Session was successfully updated");
});
deferred.fail(function () {
  alert("Group Session synchronization failed");
});
```

### `jatos.groupSession.clear(onSuccess, onFail)`

Clears the whole Group Session data and sets it to an empty object `{}`.

* _@param {optional callback} onSuccess_ - Function to be called if this patch was successfully applied on the server and the client side
* _@param {optional callback} onError_ - Function to be called if this patch failed
* _@return {jQuery.deferred.promise}_

Example:

```javascript
jatos.groupSession.clear();
```

Since there is a slight chance that the session update was not successful it's a good idea to provide callback functions for both cases. To provide success or fail callback functions you can either specify the onSuccess/onError parameters or use [jQuery' deferred object](https://api.jquery.com/deferred.promise/).

Example with jQuery's defered:

```javascript
var deferred = jatos.groupSession.clear();
deferred.done(function () {
  alert("Group Session was successfully updated");
});
deferred.fail(function () {
  alert("Group Session synchronization failed");
});
```
