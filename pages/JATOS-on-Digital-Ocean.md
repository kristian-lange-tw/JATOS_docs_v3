---
title: JATOS on Digital Ocean
keywords: install, server, digital, ocean, caddy, caddyfile, docker, deploy
tags:
summary:
sidebar: mydoc_sidebar
permalink: JATOS-on-Digital-Ocean.html
folder:
toc: true
last_updated: 12 Dec 2018
---

* If domain name: Point a and AAAA record to IP4 and IP6

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

# Get the Caddy install script and run it
bash <(curl -s https://gist.githubusercontent.com/kristian-lange/c5a7e0ed5a01b7fd726f873f81b585a5/raw/ac84589b4e50d5c0e574147f39ae32dec168cd35/caddy.sh)

# Pull and run JATOS docker container
docker pull jatos/jatos:latest
docker run -d --restart=always -p 9000:9000 jatos/jatos:latest
```
