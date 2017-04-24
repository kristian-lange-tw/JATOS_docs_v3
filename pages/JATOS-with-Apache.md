---
title: JATOS with Apache
keywords: apache, server, httpd, installation
tags:
summary:
sidebar: mydoc_sidebar
permalink: JATOS-with-Apache.html
folder:
toc: false
last_updated: 29 Dec 2016
---

This is an example for a configuration of [Apache](https://httpd.apache.org/) as a proxy in front of JATOS. It is not necessary to run JATOS with a proxy but it's common.

The following is the content of Apache's `httpd.conf`. Change it to your needs. You probably want to change your servers address (`www.example.com` in the example). If you want to use JATOS with group studies you have to add the [mod_proxy_wstunnel module](https://httpd.apache.org/docs/2.4/mod/mod_proxy_wstunnel.html).

~~~ shell
LoadModule proxy_module modules/mod_proxy.so
…
<VirtualHost *:80>
  ProxyPreserveHost On
  ServerName www.example.com
  ProxyPass  /excluded !
  ProxyPass / http://127.0.0.1:9000/
  ProxyPassReverse / http://127.0.0.1:9000/
</VirtualHost>
~~~
