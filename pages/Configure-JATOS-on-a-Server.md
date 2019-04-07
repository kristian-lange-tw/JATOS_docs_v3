---
title: Configure JATOS on a Server
keywords: server, configuration, MySQL, H2, database, study assets, study assets root, port, password, IP, port, localhost, domain, 127.0.0.1
tags:
summary: If JATOS runs locally it's usually not necessary to change the defaults. On a server, you may want to set up the IP and port, or use a different database, change the path of the study assets root folder, or add some password restrictions.
sidebar: mydoc_sidebar
permalink: Configure-JATOS-on-a-Server.html
folder:
toc: true
last_updated: 23 Mar 2019
---

**Restart JATOS after making any changes to the configuration (`loader.sh restart`)**

### IP / domain and port

By default JATOS binds to all locally available IP addresses including 127.0.0.1 on port 9000. If you don't want to use a proxy in front of JATOS, you have several ways to configure the host name or IP address and the port:

1. **Since JATOS 3.3.5** it is possible to set up IP and port via `conf/production.conf`: Edit `play.server.http.address` and `play.server.http.port` and restart JATOS. E.g. to run on IP 192.168.0.100 and port 80:

   ~~~ bash
   play.server.http.address = "192.168.0.100"
   play.server.http.port = 80
   ~~~
  
1. Via command-line arguments `-Dhttp.address` and `-Dhttp.port`, e.g. with the following command you'd start JATOS with IP 10.0.0.1 and port 80

   ~~~ bash
   loader.sh start -Dhttp.address=10.0.0.1 -Dhttp.port=80
   ~~~
   
1. (DEPRECATED) In `loader.sh` change the values of 'address' and 'port' according to your IP address or domain name and port. Restart JATOS after editing.

   ~~~ bash
   address="172.16.0.1"
   port="8080"
   ~~~   
     
### URL base path (JATOS >= v3.3.1)

JATOS can be configured to use an base path. E.g we have the host "www.example.org" and let JATOS run under "mybasepath" so that JATOS' URL all start with "www.example.org/mybasepath/". This can be achieved in two ways:

1. Via the command-line argument `-DJATOS_URL_BASE_PATH`, e.g.

   ~~~ bash
   loader.sh start -DJATOS_URL_BASE_PATH="/mybasepath/"
   ~~~

1. Via `conf/production.conf`: change `play.http.context`

   ~~~ bash
   play.http.context = "/mybasepath/"
   ~~~

**The path always has to start and end with a "/".** And keep in mind that if you add a base path to JATOS' URL you have to adjust all absolute paths to the study assets (in HTML and JavaScript files) too - [or use relative paths](Adapt-Pre-written-Code-to-run-it-in-JATOS.html#create-the-study-in-jatos).

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
     
### MySQL Database

There are three ways to set up JATOS to work with an MySQL:

1. Via command-line arguments:
   * `-DJATOS_DB_URL` - specifies the JDBC URL to the database
   * `-DJATOS_DB_USERNAME` and `-DJATOS_DB_PASSWORD` - set username and password
   * `-DJATOS_DB_DRIVER` - can be either `org.h2.Driver` or `com.mysql.jdbc.Driver`
   * `-DJATOS_JPA` - can be either `h2PersistenceUnit` or `mysqlPersistenceUnit`
   
   E.g. to connect to a MySQL running on 172.17.0.2 use:
   
   ~~~ bash
   loader.sh start -DJATOS_DB_URL='jdbc:mysql://172.17.0.2/jatos?characterEncoding=UTF-8' -DJATOS_DB_USERNAME=sa -DJATOS_DB_PASSWORD=sa -DJATOS_JPA=mysqlPersistenceUnit -DJATOS_DB_DRIVER=com.mysql.jdbc.Driver
   ~~~
   
1. Via `conf/production.conf` (change IP and 'mypassword')

   ~~~ bash
   db.default.url="jdbc:mysql://172.17.0.2/MyDatabase?characterEncoding=UTF-8"
   db.default.user=jatosuser
   db.default.password=mypassword
   db.default.driver=com.mysql.jdbc.Driver
   jpa.default=mysqlPersistenceUnit
   ~~~
   
1. Via environment variables
   * `JATOS_DB_URL`
   * `JATOS_DB_USERNAME`
   * `JATOS_DB_PASSWORD`
   * `JATOS_DB_DRIVER`
   * `JATOS_JPA`
   
   E.g. to set all database environment variables for a MySQL you could use a command (change IP and 'mypassword'):
   
   ~~~ bash
   export JATOS_DB_URL='jdbc:mysql://172.17.0.2/jatos?characterEncoding=UTF-8' JATOS_DB_USERNAME='jatosuser' JATOS_DB_PASSWORD='mypassword' JATOS_DB_DRIVER=com.mysql.jdbc.Driver JATOS_JPA=mysqlPersistenceUnit
   ~~~
   
You can confirm that JATOS is accessing the correct database by looking in the logs. One of the lines after JATOS starts should look like this (with your JDBC URI).

~~~ bash
19:03:42.000 [info] - p.a.d.DefaultDBApi - Database [default] connected at jdbc:mysql://localhost/jatos?characterEncoding=UTF-8
~~~  

### Password restrictions

By default JATOS' keeps it simple and relies on the users to choose save passwords: it just enforces a length of at least 7 characters. But this can be changed in the `conf/production.conf` with the following two properties.

* `jatos.user.password.length` - Set with an positive integer (default is 7)
* `jatos.user.password.strength` - Set to 0, 1, 2, or 3 (default is 0)
  * `0`: No restrictions on characters
  * `1`: At least one Latin letter and one number
  * `2`: At least one Latin letter, one number and one special character (`#?!@$%^&*-`)
  * `3`: At least one uppercase Latin letter, one lowercase Latin letter, one number and one special character (`#?!@$%^&*-`)

### Other configuration in production.conf

Additional to the [database](#Database) and the [study assets root path](#study-assets-root-path) some other properties can be configured in the `conf/production.conf`.

* `jatos.userSession.timeout` - time in minutes a user stays logged in (default is 1440 = 1 day)
* `jatos.userSession.inactivity` - defines the time in minutes a user is automatically logged out after inactivity (default is 60)
* `jatos.userSession.validation` - (since JATOS >= 3.1.10) - toggles user session validation: set to false to switch it off (default is true) - WARNING: Turning off the user session validation reduces JATOS security! Sometimes this is necessary, e.g. if your users have a extremely dynamic IP address.
* `play.http.session.secure` - secure session cookie: set true to restrict user access to HTTPS (default is false)

Apart from those all [configuration properties possible in the Play Framework](https://www.playframework.com/documentation/latest/Configuration) are possible in JATOS production.conf too. 


