---
title: JATOS with Apache
keywords: apache, server, httpd, installation, websocket, proxy, mod_proxy_wstunnel module
tags:
summary:
sidebar: mydoc_sidebar
permalink: JATOS-with-Apache.html
folder:
toc: false
last_updated: 3 April 2017
---

This is an example of a configuration of [Apache](https://httpd.apache.org/) as a proxy in front of JATOS. While it's not necessary to run JATOS with a proxy, it's common to do so in order to allow encryption.

Here I used Apache 2.4.18 on a Ubuntu system. I recommend to use at least **version 2.4** since JATOS relies on WebSockets, not supportted by earlier Apache versions. 

I had to add some modules to Apache to get it working:

~~~ shell
sudo a2enmod rewrite
sudo a2enmod proxy_wstunnel
sudo a2enmod proxy
sudo a2enmod headers
sudo a2enmod ssl
sudo a2enmod lbmethod_byrequests
sudo a2enmod proxy_balancer
sudo a2enmod proxy_http
sudo a2enmod remoteip
~~~

The following is an example of a proxy config with Apache. I stored it in `/etc/apache2/sites-available/example.com.conf` and added it to Apache with the command `sudo a2ensite example.com.conf`. It enforces access via HTTPS by redirecting all HTTP traffic.

~~~ shell
<VirtualHost *:80>
  ServerName www.example.com
  
  # Redirect all unencrypted traffic to the respective HTTPS page
  Redirect "/" "https://www.example.com/"
</VirtualHost>

<VirtualHost *:443>
  ServerName www.example.com

  # Needed for JATOS to get the correct host and protocol
  ProxyPreserveHost On
  RequestHeader set X-Forwarded-Proto "https"
  RequestHeader set X-Forwarded-Ssl "on"
  
  # Your certificate for encryption
  SSLEngine On
  SSLCertificateFile /etc/ssl/certs/localhost.crt
  SSLCertificateKeyFile /etc/ssl/private/localhost.key

  # JATOS uses WebSockets in its group studies
  RewriteEngine On
  RewriteCond %{HTTP:Upgrade} =websocket [NC]
  RewriteRule /(.*)           ws://localhost:9000/$1 [P,L]
  RewriteCond %{HTTP:Upgrade} !=websocket [NC]
  RewriteRule /(.*)           http://localhost:9000/$1 [P,L]

  # Proxy everything to the JATOS running on localhost on port 9000
  ProxyPass / http://localhost:9000/
  ProxyPassReverse / http://localhost:9000/
</VirtualHost>
~~~
