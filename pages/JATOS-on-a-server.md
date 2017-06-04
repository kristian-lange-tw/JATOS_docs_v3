---
title: JATOS on a server
keywords: server, installation, test, config, configuration
tags:
summary: To run studies online, e.g. with Mechanical Turk, JATOS has to be installed on a server. Server instances of JATOS have slightly different configuration requirements than local instances. This text aims at server admins who wants to setup a server running JATOS and who know their way around server management.
sidebar: mydoc_sidebar
permalink: JATOS-on-a-server.html
folder:
toc: true
last_updated: 28 Apr 2017
---

There are several ways to bring JATOS to the internet. You can install it

* on your own dedicated server
* in the cloud (with IaaS)
* in the cloud with a Docker container

The first two are discussed here in this page. The last one has its own [page](Install-JATOS-via-Docker.html).

One word about IaaS. There are many IaaS providers (Digital Ocean, Microsoft Azure, Google Cloud, Amazon's AWS etc.). They all give you some kind of virtual machine (VM) and the possibility to install an operating system on it. I'd recommend to go with a Linux system like Ubuntu or Debian. Another point is to make sure they have persistent storage and not what is often called 'ephemeral storage' (storage that is deleted after the VM shuts down). Since JATOS stores all study assets in the server's file system persistent storage is needed. But apart from that it's the same JATOS installation like on a dedicated server. In [JATOS in Amazon's Cloud (without Docker)](JATOS-in-Amazons-Cloud-without-Docker.html) we have some advice in how to do it in AWS. 

The actual JATOS instance on a server isn't too different from a local one. It basically involves telling JATOS which IP address and port it should use and (optionally) replace the H2 database with a MySQL one. There are other issues however, not directly related to JATOS, that you should consider when setting up a server. These include: setting up automatic, regular backups of your data, an automatic restart of JATOS after a server reboot, encryption, additional HTTP server, etc.

## Installation on a server

### 1. Install Java

We've produced multiple versions of JATOS. The simplest version is JATOS alone, but other versions are bundled with Java JRE. On a server, it's best (though not necessary) to install JATOS without a bundled Java. This will make it easier to upgrade to new Java releases.

### 2. Install JATOS

1. [Download JATOS](https://github.com/JATOS/JATOS/releases)
1. JATOS comes zipped. Unpack this file at a location in your server's file system where JATOS should be installed.
1. Check that the file `loader.sh` in the JATOS folder is executable.
1. Check that JATOS starts with `loader.sh start|restart|stop`

### 3. Configuration
If JATOS runs locally it's usually not necessary to change the defaults but on a server you probably want to set up the IP and port or maybe use a different database and change the path of the study assets root folder. These docs have an extra page on how to [Configure JATOS on a Server](Configure-JATOS-on-a-Server.html).

### 4. Change Admin's password
Every JATOS installation comes with an Admin user that has the default password 'admin'. You must change it before the server goes live. This can be done in JATOS' GUI:

1. Start JATOS and in a browser go to JATOS login page `http://your-domain-or-IP/jatos` 
1. Login as 'admin' with password 'admin'
1. Click on 'Admin (admin) in top-right header
1. Click 'Change Password'

### 5. Check JATOS' test page
JATOS comes with a handy test page `http://your-domain-or-IP/jatos/test`. It shows some of the current configuration and system properties. Above all it does some tests, e.g. WebSockets connections and database connection. Check that all tests show an 'OK'.

### 6. [Optional] HTTP server and encryption
Most admins tend to use an additional HTTP server in front of JATOS for encryption purpose. We provide two example configurations for Nginx and Apache. Both support encryption and WebSockets (keep in mind JATOS relies on WebSockets and it's necessary to support them). 

* [JATOS with Nginx](JATOS-with-Nginx.html)
* [JATOS with Apache](JATOS-with-Apache.html)

### 7. [Optional] Auto-start JATOS

It's nice to have JATOS starts automatically after a start or a reboot of your machine. It's easy to turn the `loader.sh` script into an init script for a daemon.

1. Copy the `loader.sh` script to `/etc/init.d/`
1. Rename it to `jatos`
1. Change access permission with `chmod og+x jatos`
1. Edit `/etc/init.d/jatos`
   1. Comment out the line that defines the JATOS location `dir="$( cd "$( dirname "$0" )" && pwd )"`
   1. Add a new locatoin `dir=` with the path to your JATOS installation

      The beginning of your `/etc/init.d/jatos` should look like:
  
      ~~~ shell
      #!/bin/bash
      # JATOS loader for Linux and MacOS X
      
      # Change IP address and port here
      # Alternatively you can use command-line arguments -Dhttp.address and -Dhttp.port
      address="127.0.0.1"
      port="9000"
      
      # Don't change after here unless you know what you're doing
      ###########################################################

      # Get JATOS directory
      #dir="$( cd "$( dirname "$0" )" && pwd )"
      dir="/path/to/my/JATOS/installation"
      ...
      ~~~
  
1. Make it auto-start with the command `sudo update-rc.d jatos defaults`

Now JATOS starts automatically when you start your server and stops when you shut it down. You can also use the init script yourself like any other init script with `sudo /etc/init.d/jatos start|stop|restart`.

### 8. [Optional] Backup

There is always the possibility that JATOS's users care themselves for their data. JATOS has an easy to use [export function for result data](Manage-results.html). So you could just tell everyone to export their data regularily.

But if you want to set up a regular backup of the data stored in JATOS here are the necessary steps. Those data consists of two parts (1.) the data stored in the database and (2.) your study assets folder that contains all the web files (e.g. HTML, JavaScript, images). Both have to be backed up to be able to restore them later on.

1. **Database**
    * **MySQL** - If you use a MySQL database you might want to look into the `mysqldump` shell command. E.g., with `mysqldump -u myusername -p mydbname > mysql_bkp.out` you can backup the whole data into a single file. Restore the database with `mysql -u myusername -p mydbname < mysql_bkp.out`.
    * **H2** - There are at least two ways: one easy (but unofficial) and one official:
      1. Copy & paste the db file - It's important to **stop JATOS** before doing a backup or restoring a H2 database this way. If you do not stop JATOS your [data might be corrupted](Troubleshooting.html#database-is-corrupted). You can just backup the folder `my-jatos-path/database`. In case you want to restore an older version from the backup just replace the current version of the folder with the backed-up version.
      1. Via [H2's upgrade, backup, and restore tool](http://www.h2database.com/html/tutorial.html#upgrade_backup_restore)

1. **Study assets root folder** - You can just make a backup of your study assets folder. If you want to return to a prior version replace the current folder with the backed-up version.

Remember, a backup has to be done of **both** the _database_ **and** the _study assets root folder_.
