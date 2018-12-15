---
title: JATOS on Digital Ocean
keywords: install, server, digital, ocean, caddy, caddyfile, docker, deploy
tags:
summary:
sidebar: mydoc_sidebar
permalink: JATOS-on-Digital-Ocean.html
folder:
toc: true
last_updated: 15 Dec 2018
---

[Digital Ocean](https://cloud.digitalocean.com) comparatively easy to use and great documentation: One-Click Droplets with Docker 
(there are others - no affiliation)

Droplet just a server in the cloud. Privacy concerns.

Cost money (not a lot) - needs a credit card!

Prerequisites
* Digital Ocean account

## Digital Ocean setup

* Droplet with One-Click App has one with Ubuntu + Docker: https://cloud.digitalocean.com/droplets/new?image=docker-18-04
* Photo: One-Click App
* Choose a size: JATOS usually runs with 1 GB memory, 1 CPU - the smallest usually fine (currently 5$ / month)
* Photo
* Choose region (any, but near to your participants best)
* Photo
* Select additional options: add **User Data**
* Photo 

```shell
#!/bin/bash

# Run JATOS as docker container
docker pull jatos/jatos:latest
docker run -d --restart=always -p 80:9000 jatos/jatos:latest
```

* Optional add SSH key and change droplet's name
* Click 'Create'
* Email with something similar to this (if no SSH key provided)

> Your new Droplet is all set to go! You can access it using the following credentials:
> 
> Droplet Name: docker-s-1vcpu-1gb-fra1-01
> IP Address: xx.xx.xx.xx
> Username: root
> Password: xxxxxxxxxxxxxxxxxxxxxxxxx

* Should run out of the box: go to your browser and use the _IP Address_
* Further setup: Access via SSH root and your password

## HTTPS with Caddy

[Caddy](https://caddyserver.com/) as a proxy: adds encryption (HTTPS) out-of-the-box

Prerequisites:
* Needs domain name: get one yourself or from your institute or from me(?)
* Caddy's license: only **free for private or academic use** (https://caddyserver.com/products/licenses)

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

* If domain name: Point a and AAAA record to IP4 and IP6
