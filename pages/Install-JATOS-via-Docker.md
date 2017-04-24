---
title: Install JATOS via Docker
keywords: docker, container, installation, server
tags:
summary:
sidebar: mydoc_sidebar
permalink: Install-JATOS-via-Docker.html
folder:
toc: true
last_updated: 29 Dec 2016
---

JATOS has a Docker image: [hub.docker.com/r/jatos/jatos/](https://hub.docker.com/r/jatos/jatos/)

Docker is a great technology, but if you never heard of it you can safely ignore this page (it's not necessary to use it if you want to install JATOS, either locally or on a server). 

If you have heard of it, you might want to, for example, setup JATOS in a Docker container together with an external H2 or MySQL database in another Docker container. You can easily do that: 

### Install JATOS locally with a Docker container

1. Install Docker locally on your computer (not covered here)

1. Go to your shell or command line interface

1. Pull the JATOS image: use `docker pull jatos/jatos:x.x.x` and specify the release, e.g. to get version 2.2.4 use `docker pull jatos/jatos:2.2.4`

1. Check that you actually downloaded the image: `docker images` should show `jatos/jatos` in one line

1. Now run JATOS (and create a new Docker container) with `docker run -d -p 9000:9000 jatos/jatos:x.x.x`, e.g. to for version 2.2.4 use `docker run -d -p 9000:9000 jatos/jatos:2.2.4`. The `-d` argument specifies to run this container as a daemon and the `-p` is responsible for the port mapping.

1. Check that the new container is running: In your browser go to [localhost:9000](http://localhost:9000) - it should show the JATOS login screen. Or use `docker ps -a` - in the line with `jatos/jatos` the status should say `up`.

**Troubleshooting**: By removing the `-d` argument (e.g. `docker run -p 9000:9000 jatos/jatos:2.2.4`) you get JATOS' logs printed in your shell - although you don't run it as a daemon in the background anymore.  

### Change port

With Docker you can easily change JATOS' port (actually we change the port mapping of JATOS' docker container). Just use Docker `-p` argument and specify your port. E.g. to run JATOS on port 8080 use `docker run -d -p 8080:9000 jatos/jatos:2.2.4`.

### Configure with environment variables

All environment variables that can be used to [configure a normal JATOS server installation](Configure-JATOS-on-a-Server.html) can be used in a docker installation. Just use Docker's `-e` argument to set them.

E.g. to setup JATOS with a MySQL database running under IP `172.17.0.2` that uses the table `jatos` use the following command (but change the JATOS version and use username and password of your MySQL account):

~~~ shell
docker run -e JATOS_DB_URL='jdbc:mysql://172.17.0.2/jatos?characterEncoding=UTF-8' -e JATOS_DB_USERNAME='root' -e JATOS_DB_PASSWORD='password' -e JATOS_DB_DRIVER=com.mysql.jdbc.Driver -e JATOS_JPA=mysqlPersistenceUnit -p 9000:9000 jatos/jatos:2.2.4
~~~
