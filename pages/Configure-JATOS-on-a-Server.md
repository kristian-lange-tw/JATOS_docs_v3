---
title: Configure JATOS on a Server
keywords: server, configuration, MySQL, H2, database, study assets, study assets root, port
tags:
summary: If JATOS runs locally it's usually not necessary to change the defaults. On a server, you probably will want to set up the IP and port, or use a different database and change the path of the study assets root folder.
sidebar: mydoc_sidebar
permalink: Configure-JATOS-on-a-Server.html
folder:
toc: true
last_updated: 29 Dec 2016
---

**Restart JATOS after making any changes to the configuration (`loader.sh restart`)**

### IP / domain and port

By default JATOS uses the address 127.0.0.1 and port 9000. There are two ways to configure the host name or IP address and the port:

1. In `loader.sh` change the values of 'address' and 'port' according to your IP address or domain name and port.

   ~~~ bash
   address="172.16.0.1"
   port="8080"
   ~~~
  
1. Via command-line arguments `-Dhttp.address` and `-Dhttp.port`, e.g. with the following command you'd start JATOS with IP 10.0.0.1 and port 80

   ~~~ bash
   loader.sh start -Dhttp.address=10.0.0.1 -Dhttp.port=80
   ~~~
     
### Study assets root path

By default the study assets root folder (where all your study's HTML, JavaScript files etc. are stored) is located within JATOS installation's folder in `study_assets_root`. There are three ways to change this path:

1. Via the command-line argument `-DJATOS_STUDY_ASSETS_ROOT_PATH`, e.g.

   ~~~ bash
   loader.sh start -DJATOS_STUDY_ASSETS_ROOT_PATH="/path/to/my/assets/root/folder"
   ~~~
   
1. Via `conf/production.conf`: change `jatos.studyAssetsRootPath`

   ~~~ bash
   jatos.studyAssetsRootPath="/path/to/my/jatos_study_assets_root"
   ~~~
   
1. Via the environment variable `JATOS_STUDY_ASSETS_ROOT_PATH`, e.g. the following export adds it to the env variables:

   ~~~ bash
   export JATOS_STUDY_ASSETS_ROOT_PATH="/path/to/my/assets/root/folder"
   ~~~
     
### Database

By default JATOS uses an embedded H2 database, but it can be easily configured to work with an external H2 or a MySQL database. 

You can confirm that JATOS is accessing the correct database by looking in the logs. One of the lines after JATOS starts should look like this (with your JDBC URL).

~~~ bash
19:03:42.000 [info] - p.a.d.DefaultDBApi - Database [default] connected at jdbc:mysql://localhost/jatos?characterEncoding=UTF-8
~~~

**JATOS requires MySQL >= 5.5 or H2 >= 1.4.192 (prior versions might work - I just never tested)**

Note: If you want to use a MySQL database consider using the [_utf8mb4_ Character Set with 4-Byte UTF-8 Unicode Encoding](https://dev.mysql.com/doc/refman/5.5/en/charset-unicode-utf8mb4.html). Only this character set contains the whole unicode and you won't run into issues like [this one](https://github.com/JATOS/JATOS/issues/111). 

There are three ways to set up the database.

1. Via command-line arguments:
   * `-DJATOS_DB_URL` - specifies the JDBC URL to the database
   * `-DJATOS_DB_USERNAME` and `-DJATOS_DB_PASSWORD` - set username and password
   * `-DJATOS_DB_DRIVER` - can be either `org.h2.Driver` or `com.mysql.jdbc.Driver`
   * `-DJATOS_JPA` - can be either `h2PersistenceUnit` or `mysqlPersistenceUnit`
   
   E.g. to connect to a MySQL database running on 172.17.0.2 and a table named 'jatos' use:
   
   ~~~ bash
   loader.sh start -DJATOS_DB_URL='jdbc:mysql://172.17.0.2/jatos?characterEncoding=UTF-8' -DJATOS_DB_USERNAME=sa -DJATOS_DB_PASSWORD=sa -DJATOS_JPA=mysqlPersistenceUnit -DJATOS_DB_DRIVER=com.mysql.jdbc.Driver
   ~~~
1. Via production.conf (description analog to 1.)

   ~~~ bash
   db.default.url="jdbc:mysql://localhost/MyDatabase?characterEncoding=UTF-8"
   db.default.user=myusername
   db.default.password=mypassword
   db.default.driver=com.mysql.jdbc.Driver
   jpa.default=mysqlPersistenceUnit
   ~~~
   
1. Via environment variables (description analog to 1.)
   * `JATOS_DB_URL`
   * `JATOS_DB_USERNAME`
   * `JATOS_DB_PASSWORD`
   * `JATOS_DB_DRIVER`
   * `JATOS_JPA`
   
   E.g. to set all database environment variables for a MySQL database and table called 'jatos' you could use a command (change the values):
   
   ~~~ bash
   export JATOS_DB_URL='jdbc:mysql://localhost/jatos?characterEncoding=UTF-8' JATOS_DB_USERNAME='jatosuser' JATOS_DB_PASSWORD='mypassword' JATOS_DB_DRIVER=com.mysql.jdbc.Driver JATOS_JPA=mysqlPersistenceUnit
   ~~~
     
