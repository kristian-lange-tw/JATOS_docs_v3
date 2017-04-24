---
title: JATOS in Amazon's Cloud (without Docker)
keywords: cloud, aws, amazon, installation, server
tags:
summary:
sidebar: mydoc_sidebar
permalink: JATOS-in-Amazons-Cloud-without-Docker.html
folder:
toc: false
last_updated: 29 Dec 2016
---

On this page is additional information in how to install JATOS on a server in Amazon's Web Services. All general installation advice is in [JATOS on a server](JATOS-on-a-server.html) and applies here too.

1. First you need to register at [AWS (Amazon Web Services)](https://aws.amazon.com/) (they'll want your credit card).
1. In AWS webpage move to EC2 and launch a new instance with Ubuntu (you can use other Linux too - I tested it with Ubuntu 14.04)
1. During the creation of the new EC2 instance you will be ask whether you want to create a key pair. Do so. Download the file with the key (a *.pem file). Store it in a safe place - with this key you will access your server.
1. Login via SSH: `ssh -i /path/to/your/pem_key_file ubuntu@xx.xx.xx.xx` (Use your instance's IP address: In AWS / EC2 / Instances / Description are two IPs 'Private IP' and 'Public IP'. Use the **public** one.)
1. Get the latest JATOS bundled with Java (exchange x.x.x with the version you want) `wget https://github.com/JATOS/JATOS/releases/download/vx.x.x/jatos-x.x.x-linux_java.zip`
1. `unzip jatos-x.x.x-linux_java.zip` (You probably have to install 'unzip' first with `sudo apt-get install unzip`.)
1. Configure IP and port in `jatos.sh`: Use the '**Private IP**' from your instance description (the one that starts with 172.x.x.x) and port 80
1. (Optional) [make JATOS auto-start](JATOS-on-a-server.html#auto-start-jatos-on-linuxunix-as-a-daemon)
1. Change JATOS' admin password
