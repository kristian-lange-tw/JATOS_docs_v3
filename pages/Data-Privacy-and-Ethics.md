---
title: Data Privacy and Ethics
keywords: privacy, ethics
tags:
summary:
sidebar: mydoc_sidebar
permalink: Data-Privacy-and-Ethics.html
folder:
toc: false
last_updated: 29 Dec 2016
---

Data privacy is a critical issue in online studies. You should be careful when collecting, storing and handling data, regardless of which platform you use to run your studies. 

We developed JATOS with data privacy in mind, preventing any breaches of the standard ethical principles in research. However, ultimately you are responsible for the data you collect and what you do with it. 

![GUI Screenshot](images/IMG_1376.JPG)

(copyright 2006 John klossner, www.jklossner.com)

Here are a few advantages and limitations of JATOS with regards to data privacy. Please read them carefully before you run any study, and please [contact us](Contact-us.html) if you find that these are not sufficient, or have suggestions for improvement.  

* JATOS' main advantage is that you can store your participants' data in your own server, and not in a commercial server like Amazon or Qualtrics. This means that you have full control over the data stored in your database, and no commercial company has access to it. 

* By default, JATOS stores the following data: 
  * time (of the server running JATOS) at which the study -and each of its components- was started and finished
  * the [worker type](Worker-Types.html) (MTurk, General single, Personal multiple, etc) 
  * in cases of MTurk workers, the confirmation code AND the MTurk worker ID. In these cases, if an MTurk worker participated in two of your studies, running in the same JATOS instance, <b>you will be able to associate the data across these two studies</b>. This is an important issue: MTurk workers might not be aware that you are the same researcher, and will not know that you have the chance to associate data from different studies. The best way to avoid this is to export all your study's data and delete it from the JATOS database once you are done with it. In this way, JATOS won't know that a worker already participated in another study and will create a new worker ID for them.   

* JATOS will <b>not</b> store information like IP address or browser type. However, you could access and store this information through your JavaScripts. You could also record whether workers are actively on the browser tab running your study, or whether they have left it to go to another tab, window or program. If you collect any of these data, you should let your workers know. 

* Bear in mind: Every file within your study assets folders is public to the Internet. Anybody can in principle read any file in this folder, regardless of how secure your server is. **Thus, you should never store any private data, such as participants' details in the study assets folders.**

### Things you should consider in your studies 

* You should consider to add some button in your study pages to abort the study. Some ethics demand that any participant should have the **right to withdraw** at any time, without explanation. In this case all data of the participant gathered during the study should be deleted. Conveniently jatos.js offers an [abortStudy method](jatos.js-Reference.html#jatosabortstudymessage).

* Use **encryption** with your [server instance](JATOS-on-a-server.html). Only with encryption no one else in the internet can read the private data from your study's participants. 
