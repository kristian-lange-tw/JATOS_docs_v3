---
title: JATOS on a server
keywords: server, installation
tags:
summary: To run studies online, e.g. with Mechanical Turk, JATOS has to be installed on a server. Server instances of JATOS have slightly different configuration requirements than local instances. This text aims at server admins who wants to setup a server running JATOS and who know their way around server management.
sidebar: mydoc_sidebar
permalink: JATOS-on-a-server.html
folder:
toc: true
last_updated: 29 Dec 2016
---

There are several ways to bring JATOS to the internet. You can install it

* on your own dedicated server
* in the cloud on an Infrastructure as a Service (IaaS)
* in the cloud with a Docker container

The first two are discussed here in this page. For the last one JATOS provides a [Docker image](Install-JATOS-via-Docker.html).

One word about IaaS. There are many IaaS providers (Digital Ocean, Microsoft Azure, Google Cloud, Amazon's AWS etc.). They all give you a virtual machine (VM) and the possibility to install an operating system on it. I'd recommend to go with a Linux system like Ubuntu or Debian. Another point is to make sure they have persistent storage and not what is often called 'ephemeral storage' (storage that is deleted after the VM shuts down). Since JATOS stores all study assets in the server's file system persistent storage is needed. But apart from that it's the same JATOS installation like on a dedicated server. In [JATOS in Amazon's Cloud (without Docker)](JATOS-in-Amazons-Cloud-without-Docker.html) we have some advice in how to do it in AWS. 

The actual JATOS instance on a server isn't too different from a local one. It basically involves telling JATOS which IP address and port it should use and (optionally) replace the H2 database with a MySQL one. There are other issues however, not directly related to JATOS, that you should consider when setting up a server. These include: setting up automatic, regular backups of your data, an automatic restart of JATOS after a server reboot, encryption, additional HTTP server, etc. The purpose of this page is not to teach you how to set up a server in general (you do need to know a little bit about Internet and security issues and should not try it at home unless you know what you're doing!). Here, we simply cover the steps to server setup that are related to JATOS. 

### Java
We've produced multiple versions of JATOS. The simplest version is JATOS alone, but other versions are bundled with Java JRE. On a server, it's best (though not necessary) to install JATOS without a bundled Java. This will make it easier to upgrade to new Java releases.

### Configuration
If JATOS runs locally it's usually not necessary to change the defaults but on a server you probably want to set up the IP and port or maybe use a different database and change the path of the study assets root folder. These docs have an extra page on how to [Configure JATOS on a Server](Configure-JATOS-on-a-Server.html).

### Change admin's password
Every JATOS installation has the same default admin password 'admin'. You must change it before the server goes live. This can be done in the GUI: 1) login as 'admin', 2) click on your user in the header 3) Click 'Change Password'. 

### Backup
You should set up a regular backup of your data from JATOS. These include (1.) the data stored in the database and (2.) your study assets folder.

1. If you use the default H2 database you can just backup the folder `my-jatos-path/database`. In case you want to restore an older version from the backup just replace the current version of the folder with the backed-up version. If you use a MySQL database you might want to look into the `mysqldump` shell command. E.g., with `mysqldump -u myusername -p mydbname > mysql_bkp.out` you can backup the whole data into a single file. Restore the database with `mysql -u myusername -p mydbname < mysql_bkp.out`.

1. You can just make a backup of your study assets folder. If you want to return to a prior version replace the current folder with the backed-up version.

Remember, a backup has to be done of **both** the database **and** the study assets root folder.

### HTTP server
JATOS doesn't need an HTTP server (like Nginx or Apache). It is its own HTTP server. But sometimes it is necessary to have an additional server in front of JATOS (e.g. for HTTPS encryption). In [JATOS with Nginx](JATOS-with-Nginx.html) we show a sample configuration for Nginx and in [JATOS with Apache](JATOS-with-Apache.html) for Apache. And keep in mind that JATOS uses WebSockets for group studies and your HTTP server should be configured to support them.

### Auto-start JATOS on Linux/Unix as a daemon

It's nice to have JATOS starts automatically after a start or a reboot of your machine. It's easy to turn the `loader.sh` script that you normally use to start JATOS into an init script for a daemon.

1. Copy the `loader.sh` script to `/etc/init.d/`
1. Rename it to `jatos`
1. Change access permission with `chmod og+x jatos`
1. Edit `/etc/init.d/jatos`
   1. Specify the IP address and port you want to use
   1. Comment out the line `dir="$( cd "$( dirname "$0" )" && pwd )"`
   1. Add variable `dir=` with the path to your JATOS installation

      The beginning of your `/etc/init.d/jatos` should look like:
  
      ~~~ 
      #!/bin/bash
      # JATOS loader for Linux and MacOS X
      
      # Change IP address and port here
      address="127.0.0.1"
      port="9000"
      dir="/path/to/my/JATOS/installation"
      
      # Don't change after here unless you know what you're doing
      #####################################
      # Get JATOS directory
      #dir="$( cd "$( dirname "$0" )" && pwd )"
      pidfile=$dir/RUNNING_PID
      ~~~
  
1. Make it auto-start with the command `sudo update-rc.d jatos defaults`

Now JATOS starts automatically when you start your server and stops when you shut it down. You can also use the init script yourself like any other init script with `sudo /etc/init.d/jatos start|stop|restart`.

### Encryption and HTTPS
Most admins tend to use an additional HTTP server in front of JATOS for encryption purpose. But since JATOS is built with the Play Framework it can be setup JATOS directly by following their [Documentation about Configuring HTTPS](https://www.playframework.com/documentation/2.4.x/ConfiguringHttps).

### JVM Memory
If your JATOS instance has a high worker load or runs many different studies, you might have to increase the memory that is available to the JVM that runs JATOS. A clear sign that your JVM needs more memory is a `java.lang.OutOfMemoryError` in your log. To increase the maximal available memory use the `-Xmx` parameter of the JVM. You can set it in the environment variable JAVA_OPTS. E.g. to set it to 2048 MB use `export set JAVA_OPTS="-Xmx2048m"` on a Linux/MacOS X system.
