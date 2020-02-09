---
title: Randomize condition assignment between-participants
keywords: between-subjects, batch session
tags:
summary:
sidebar: mydoc_sidebar
permalink: Randomize-condition-assignment-between-participants.html
folder:
toc: true
last_updated: 5 Feb 2020
---

Say you have three conditions, *A*, *B*, and *C* and you want to automatically assign half your participants to each of them. You need some way to keep track of how many participants were assigned to each condition. Because this information needs to outlive any study run, you can do it with the Batch session. 

There are of course many other ways to do the same thing, but here's one way: 

1. If the Batch Session is empty, fill it in with a 'fresh' counter, set to the maximum number of participants per condition

```
function initBatchConditions() {
		// Check if 'conditions' are not already in the batch session
		if (!jatos.batchSession.defined("/conditions")) {
			// Get the count of each condition
			var conditionCounts = jatos.componentJsonInput.conditionCounts;
			var conditions = [];
			// Fill the array with conditions according to the counters
			fillArrayWithValues(conditions, "A", conditionCounts.A);
			fillArrayWithValues(conditions, "B", conditionCounts.B);
			fillArrayWithValues(conditions, "C", conditionCounts.C);
			// Put the conditions in the batch session
			jatos.batchSession.set("conditions", conditions)
				.fail(initBatchConditions); // If it fails: try again
		}
	}
  
  function fillArrayWithValues(array, value, count) {
		for (var i = 0; i < count; i++) {
			array.push(value);
		}
	}
```

2. Find a condition with available 'slots', which you can then use in your script to decide which of your two possible conditions you'll run

```
function getNextCondition() {
		// Get the still available conditions from the Batch Session
		var conditions = jatos.batchSession.get("conditions");
		// If no more conditions throw an error
		if (conditions.length == 0) {
			$('p').text("Error: max number of workers reached.");
			throw "Max number of workers reached.";
		}
		// Get a random condition
		var randomIndex = Math.floor(Math.random() * conditions.length);
		var randomCondition = conditions[randomIndex];
		// Delete the choosen condition from the array
		conditions.splice(randomIndex, 1);
		// Set the changed conditions array in the Batch Session.
		jatos.batchSession.set("conditions", conditions).fail(function () {
			randomCondition = getNextCondition(); // If it fails: try again
		});
		return randomCondition;
	}
```


Have a look at the ["Randomize tasks between workers"](Example-Studies.html) study in our examples for the full code. 



