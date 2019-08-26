---
title: Expose your local JATOS
keywords: installation, internet, online, ngrok, serveo, localhost.run, tunnel
tags:
summary:
sidebar: mydoc_sidebar
permalink: Expose-your-local-JATOS.html
folder:
toc: true
last_updated: 26 Aug 2019
---

More information about how to [bring your JATOS online](Bring-your-JATOS-online.html)

This page is about on how to expose your locally installed JATOS to the Internet. If you want to know a bit more about the background, I recommend reading [Tunnelling services for exposing localhost to the web](https://www.chenhuijing.com/blog/tunnelling-services-for-exposing-localhost-to-the-web). There are several tunneling services and some of those are free or have at least a free offer. Here we concentrate on _Serveo_, _ngrok_, and _localhost.run_. All tree are working fine. Just pick one.

But first some general advice:

* You have to **leave your computer running** you want your participants to access your JATOS with your study. Potentially you can use your computer in the mean time, but be aware that everything might interfere with JATOS, e.g. a crashed OS stops JATOS too. Better let your computer run in peace for the duration of your study. 
* This way to bring JATOS online is the easiest to use - but also the **least reliable** one. Your local computer is prone to accidents (e.g. unplugged power cable, interrupted Internet). If you need a more dependable JATOS look at [Bring your JATOS online](Bring-your-JATOS-online.html).


## Serveo

1. Start your local JATOS

1. Execute in your terminal

   ```shell
   ssh -R 80:localhost:9000 serveo.net
   ```
   Serveo gives you an URL that is accessible from everywhere in the Internet.

   Tje output should look similar to this:

   ```shell
   $ ssh -R 80:localhost:9000 serveo.net
   Forwarding HTTP traffic from https://relego.serveo.net
   Press g to start a GUI session and ctrl-c to quit.
   ```
   
1. Copy & Paste the URL into your browser and check that JATOS is running properly with JATOS' test page _https://my-subdomain.serveo.net/jatos/test_ (exchange _my-subdomain_ with the subdomain you got in the last step)

1. That's all. Now you can [create worker links](Run-your-Study-with-Worker-and-Batch-Manager.html) and send them to your participents. Remember to use your _serveo.net_ address to create worker links.

More information on [https://serveo.net](https://serveo.net/).


## ngrok

1. Download & setup ngrok: [https://ngrok.com/download](https://ngrok.com/download)

1. I recommend creating an account with ngrok. It's free and ngrok gives you better connection compared to without.

1. Start your local JATOS

1. Start ngrok on JATOS with

   ```shell
   ./ngrok http 9000
   ```
   
   The output should look similar to this:

   ![ngrok screenshot](images/screenshot_ngrok.png)
   
1. Copy & Paste the URL with _https_ to your browser and check that JATOS is running properly with JATOS' test page _https://my-subdomain.ngrok.io/jatos/test_ (exchange _my-subdomain_ with the subdomain you got in the last step)

1. That's all. Now you can [create worker links](Run-your-Study-with-Worker-and-Batch-Manager.html) and send them to your participents. Remember to use your _ngrok.io_ address to create worker links.

More information on [https://ngrok.com](https://ngrok.com/).


## localhost.run

1. Start your local JATOS

1. Execute in your terminal

   ```shell
   ssh -R 80:localhost:9000 ssh.localhost.run
   ```

   E.g. the output could look like:
   
   ```shell
   $ ssh -R 80:localhost:9000 ssh.localhost.run
   Connect to http://kristian-44bs.localhost.run or https://kristian-44bs.localhost.run
   ```shell
   
1. Copy & Paste the URL with _https_ into your browser and check that JATOS is running properly with JATOS' test page _https://my-subdomain.localhost.run/jatos/test_ (exchange _my-subdomain_ with the subdomain you got in the last step)

1. That's all. Now you can [create worker links](Run-your-Study-with-Worker-and-Batch-Manager.html) and send them to your participents. Remember to use your localhost.run_ address to create worker links.

More information on [http://localhost.run/](http://localhost.run/).

