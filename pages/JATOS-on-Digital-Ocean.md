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

Easy admins and semi-admins


[DigitalOcean](https://www.digitalocean.com/) is a cloud provider (like AWS, Google Cloud, Azure) that is comparatively easy to use and has good and exhaustive documentation. They offer something called _Droplets_ and _One-Click Apps_ which is just a fancy name for a pre-installed server in the cloud.

Link to privacy
Link to AWS docs
Link AWS to here
Link Server installation to here

**Danger: Will cost money. A server in the cloud doesn't come for free. And you will need a credit card!**

## Prerequisites

You need to get an account with [DigitalOcean](https://www.digitalocean.com/).

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

**Voila, you have your own JATOS server.**

Now you might want to use a nicer address than an IP and add some encryption-safety with HTTPS to your server - then read on.


## Add HTTPS with Caddy and use your own domain name

This part is optional and is only necessary if you want to have your own domain name instead of an IP and encryption (HTTPS).

**BYO domain name**: Sorry we can't give you a domain name - you have to get your own. But there are plenty [domain name registrars that help you with this business](https://www.digitalocean.com/community/tutorials/how-to-point-to-digitalocean-nameservers-from-common-domain-registrars). Another option is to talk to your IT department and convince them to give you a subdomain for free.

If you've got a domain name, you have to point it to the IP address of your JATOS server. This involves dealing with things like _A records_ or _AAAA records_ or _DNS_ servers and simply can be quite annoying. You can do this with [Digital Ocean](https://www.digitalocean.com/docs/networking/dns/how-to/manage-records/) or your registar. And remember to write both, the A record for your IPv4 address, and the AAAA record for your IPv6 address. 

Now with a domain name you can encrypt your server's communication with HTTPS (HTTPS works only with a domain name and not with an IP). For this we will use [Caddy](https://caddyserver.com/). Caddy adds encryption out-of-the-box.

**Licensing: Caddy is free only for private or academic use** (https://caddyserver.com/products/licenses)

To create a JATOS server with Caddy follow the instructions in the first paragraph [Setup a simple JATOS server on DigitalOcean](#setup-a-simple-jatos-server-on-digitalocean) but in the **User Data** field of _Select additional options_ add the following script.

```shell
#!/bin/bash

# Write Caddy's config file (Caddyfile)
cat > /etc/caddy/Caddyfile <<EOF
<my.domain.name>
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

You have to exchange <my.domain.name> with your own domain name.

This script calls and runs another script that if you are interested can see under https://gist.github.com/kristian-lange/c5a7e0ed5a01b7fd726f873f81b585a5.

More about Caddy and how to configure it: https://caddyserver.com/docs/proxy. 
