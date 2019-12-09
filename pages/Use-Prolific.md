---
title: Use Prolific 
keywords: prolific
tags:
summary:
sidebar: mydoc_sidebar
permalink: Use-Prolific.html
folder:
toc: false
last_updated: 9 Dec 2019
---

It is very easy to use JATOS together with [Prolific](https://www.prolific.co/) to recruit participants. 

This is what the _New Study_ page in Prolific looks like:

![Prolific screenshot](images/Screenshot_Prolific_create_study.png)


### 1. Enter your JATOS study link

In the field under _What is the URL of your study?_ (first red box in the screenshot), enter a link to your JATOS study.You probably want a link to either a _General Single_ or a _General Multiple_ worker type (see [JATOS' worker types](Worker-Types.html) and [Run your Study with Worker & Batch Manager](Run-your-Study-with-Worker-and-Batch-Manager.html)).


### 2. Put Prolific's end page in your study's code

The second red box contains a link that you will have to include in the JavaScript of your last component. This will (re)direct the participant to a Prolific page, with information on how to claim their payment. 

All you need to do is call `jatos.endStudyAjax`, and add a callback that will replace `window.location.href` with the Prolific end page once the ajax call is `done`:

```JavaScript
jatos.endStudyAjax().done(() => {
   // Change this URL to the one you see in Prolific
   window.location.href = 'https://app.prolific.co/submissions/complete?cc=7F61EE4E'
});
```

Of course, this can also be done together with `jatos.submitResultData`. You most likely want to do this, if you want to store result data in JATOS when you finish the last component. The only reason why you might not want to do this is if you have already submitted data at some earlier point in your code, or from an earlier component:

```JavaScript
var result = { test: "some results" };
jatos.submitResultData(result)
   .done(jatos.endStudyAjax)
   .done(() => {
      // Change this URL the one you see in Prolific
      window.location.href = 'https://app.prolific.co/submissions/complete?cc=7F61EE4E'
   });
```

We provide a [Prolific example study](https://github.com/JATOS/JATOS_examples/raw/master/examples/prolific_example.zip) that you can use as a template.

