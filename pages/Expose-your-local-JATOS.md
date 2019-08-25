---
title: Expose your local JATOS
keywords: installation, internet, online, ngrok, serveo, localtunnel, tunnel
tags:
summary:
sidebar: mydoc_sidebar
permalink: Expose-your-local-JATOS.html
folder:
toc: true
last_updated: 24 Aug 2019
---

More information about how to [bring your JATOS online](Bring-your-JATOS-online.html)

On this page we will describe how to expose your locally installed JATOS to the Internet by using tunneling services. If you want to know a bit more about the background, I recommend reading [Tunnelling services for exposing localhost to the web](https://www.chenhuijing.com/blog/tunnelling-services-for-exposing-localhost-to-the-web). There are several of those and some of those are free or have a free offer. We concentrate here on Serveo, ngrok, and Localtunnel.

- leave computer with JATOS running as long as you want your participants to access it
- reliability: internet connection reset, accidental unplugging your computer during vacuuming 
- Encrypted
- easy to use, fast
- URL you can share with your participants

## Serveo

1. Start your local JATOS

1. Execute in your terminal

   ```shell
   ssh -R 80:localhost:9000 serveo.net
   ```
   Serveo gives you an URL that is accessible from everywhere in the Internet.

   E.g. the output could look like:

   ```shell
   $ ssh -R 80:localhost:9000 serveo.net
   Forwarding HTTP traffic from https://relego.serveo.net
   Press g to start a GUI session and ctrl-c to quit.
   ```
   
1. Copy & Paste the URL into your browser and check that JATOS is running properly with JATOS' test page _https://*.serveo.net/jatos/test_ (exchange * with your subdomain)


More information on [https://serveo.net](https://serveo.net/)


## ngrok

https://ngrok.com/

## Localtunnel

  - little less delay (faster)
  - easier in use (if you know how SSH)
