---
title: JATOS on DigitalOcean
keywords: install, server, cloud, digitalocean, ocean, caddy, caddyfile, docker, deploy
tags:
summary: This page describes how to install JATOS on a server in the cloud with DigitalOcean. Optionally one can enable HTTPS with Caddy which requires a domain name.
sidebar: mydoc_sidebar
permalink: JATOS-on-DigitalOcean.html
folder:
toc: true
last_updated: 15 Dec 2018
---

[DigitalOcean](https://www.digitalocean.com/) is a cloud provider (like AWS, Google Cloud, Azure) that is comparatively easy to use and has good and exhaustive documentation. They offer something called _Droplets_ and _One-Click Apps_ which is just a fancy name for a pre-installed server in the cloud.

Link to privacy
Link to AWS docs
Link AWS to here
Link Server installation to here

**Danger: Will cost money. A server in the cloud doesn't come for free. And you will need a credit card!**

## Prerequisites

Get an account with [DigitalOcean](https://www.digitalocean.com/).

## Setup a simple JATOS server on DigitalOcean

1. Use this [link](https://cloud.digitalocean.com/droplets/new?image=docker-18-04) to create a Droplet with Ubuntu and Docker pre-installed. Do not press _Create_ yet - we need to set up things first.


   Your sreen should look similar to this one: Selected One-Click App with Docker on Ubuntu
   
1. Scroll down to _Choose a size_: JATOS usually runs fine with 1 GB memory and 1 CPU - so the smallest size usually enough (currently it cost 5$/month)

   Photo

1. Scroll down to _Choose region_: You can actually choose any, but best is to choose one that is near to your participants to reduce loading time.

   Photo

1. _Select additional options_: Here activate **User Data** and add the following script in the text field

   ```shell
   #!/bin/bash
   
   # Run JATOS as docker container
   docker pull jatos/jatos:latest
   docker run -d --restart=always -p 80:9000 jatos/jatos:latest
   ```
   
   Photo

1. Optional one can an SSH key under _Add your SSH keys_. If you don't know what this is or don't want to, just ignore this - you will still be able to access the server.

1. Finally click the _Create_ button

1. Try out your JATOS: Now the server is being created which can take a couple seconds. You should get an email from DigitalOcean with your server's (aka Droplet) name, IP address, username and password. Copy the IP to your browser and if everything went well you will see a JATOS login screen.

1. Although not necessary you can access your server via SSH `ssh root@xx.xx.xx.xx` (exchange xx.xx.xx.xx with your IP). The first time it will ask you to change your password.

Voila, you have your own JATOS server. Now you might want to use a nicer address than an IP and add some encryption-safety with HTTPS to your server - then read on.


## Add HTTPS with Caddy and use your domain name

**BYO domain name**: Sorry we can't give you a domain name - you have to get your own. But there are plenty [domain name registrars that help you with this business](https://www.digitalocean.com/community/tutorials/how-to-point-to-digitalocean-nameservers-from-common-domain-registrars). Another option is to talk to your Institutes IT department and convince them to give you a subdomain for free.

If you've got a domain name you have to point this to the IP address of your JATOS server. This involves dealing with things called _A record_ or _AAAA record_ or _DNS_ servers and simply can be quite annoying. Just rem

* If domain name: Point a and AAAA record to IP4 and IP6
* HTTPS needs a domain name


[Caddy](https://caddyserver.com/) as a proxy: adds encryption (HTTPS) out-of-the-box

Prerequisites:
* Needs domain name: get one yourself or from your institute or from me(?)
* Caddy's license: only **free for private or academic use** (https://caddyserver.com/products/licenses)

uses a script to install and run Caddy: https://gist.github.com/kristian-lange/c5a7e0ed5a01b7fd726f873f81b585a5

```shell
#!/bin/bash

# Write Caddy's config file
cat > /etc/caddy/Caddyfile <<EOF
neocortex.jatos.org
proxy / localhost:9000 {
  transparent
  websocket
}
EOF

# Install a Caddy proxy
bash <(curl -s https://gist.githubusercontent.com/kristian-lange/c5a7e0ed5a01b7fd726f873f81b585a5/raw/67523ef6f7f2fb9e48436632663259d9db65eb79/caddy.sh)

# Run JATOS as docker container
docker pull jatos/jatos:latest
docker run -d --restart=always -p 9000:9000 jatos/jatos:latest
```

