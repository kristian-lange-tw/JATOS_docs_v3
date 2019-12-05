---
title: Use Prolific
keywords: prolific
tags:
summary:
sidebar: mydoc_sidebar
permalink: Use-Prolific.html
folder:
toc: false
last_updated: 5 Dec 2019
---

It is not difficult to use JATOS together with [Prolific](https://www.prolific.co/) to get your participants. 

This is what Prolific's _New Study_ page looks like:

![Prolific screenshot](images/Screenshot_Prolific_create_study.png)


### 1. Enter your JATOS study link

In Prolific's _New study_ page you have to enter your JATOS study link (first red box in the screenshot) under _What is the URL of your study?_. For the JATOS study link a _General Single_ or a _General Multiple_ worker type is probably what you want (see [JATOS' worker types](Worker-Types.html) and [Run your Study with Worker & Batch Manager](Run-your-Study-with-Worker-and-Batch-Manager.html)).


### 2. Put Prolific's end page in your study's code

The second red box contains the link of Proflic's special end page that you have to include in the last study's code. The last component, after you end the study, should redirect to Prolific's end page.

There is an [Prolific example study](https://github.com/JATOS/JATOS_examples/raw/master/examples/prolific_example.zip) you can use as a template.

Just use `jatos.endStudyAjax` and when it is done change `window.location.href` to go to Prolific's end page:

```JavaScript
jatos.endStudyAjax().done(() => {
   // Change this URL to yours from Prolific
   window.location.href = 'https://app.prolific.co/submissions/complete?cc=7F61EE4E'
});
```

And if you additionally want to send result data to JATOS you can do so with `jatos.submitResultData`:

```JavaScript
var result = { test: "some results" };
jatos.submitResultData(result)
   .done(jatos.endStudyAjax)
   .done(() => {
      // Change this URL to yours from Prolific
      window.location.href = 'https://app.prolific.co/submissions/complete?cc=7F61EE4E'
   });
```