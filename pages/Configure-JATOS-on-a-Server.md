---
title: Configure JATOS on a Server
keywords: server, configuration, config, MySQL, H2, database, study assets, study assets root, port, password, IP, port, localhost, domain, 127.0.0.1, ldap, production.conf
tags:
summary: If JATOS runs locally it's usually not necessary to change the defaults. On a server, you may want to set up the IP and port, or use a different database, change the path of the study assets root folder, or add some password restrictions.
sidebar: mydoc_sidebar
permalink: Configure-JATOS-on-a-Server.html
folder:
toc: true
last_updated: 8 May 2020
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
   * `-DJATOS_DB_URL` - specifies the URL to the database
   * `-DJATOS_DB_USERNAME` - set your username
   * `-DJATOS_DB_PASSWORD` - set your password
   * `-DJATOS_DB_DRIVER` - always `com.mysql.cj.jdbc.Driver` for MySQL
   
   E.g. to connect to a MySQL running on 127.0.0.1 and port 3306 use (change username and password):
   
   ~~~ bash   
   loader.sh start -DJATOS_DB_URL='jdbc:mysql://127.0.0.1:3306/jatos?characterEncoding=UTF-8&useSSL=false&useJDBCCompliantTimezoneShift=true&useLegacyDatetimeCode=false&serverTimezone=UTC' -DJATOS_DB_USERNAME=sa -DJATOS_DB_PASSWORD=sa -DJATOS_DB_DRIVER=com.mysql.cj.jdbc.Driver
   ~~~
   
1. Via `conf/production.conf` (change IP, port, username and password)

   ~~~ bash
   db.default.url="jdbc:mysql://127.0.0.1:3306/jatos?characterEncoding=UTF-8&useSSL=false&useJDBCCompliantTimezoneShift=true&useLegacyDatetimeCode=false&serverTimezone=UTC"
   db.default.user=jatosuser
   db.default.password=mypassword
   db.default.driver=com.mysql.cj.jdbc.Driver
   ~~~
   
1. Via environment variables (change IP, port, username and password)

   ~~~ bash
   export JATOS_DB_URL="jdbc:mysql://127.0.0.1:3306/jatos?characterEncoding=UTF-8&useSSL=false&useJDBCCompliantTimezoneShift=true&useLegacyDatetimeCode=false&serverTimezone=UTC"
   export JATOS_DB_USERNAME=jatosuser
   export JATOS_DB_PASSWORD=mypassword
   export JATOS_DB_DRIVER=com.mysql.cj.jdbc.Driver
   ~~~
   
You can confirm that JATOS is accessing the correct database by looking in the logs. One of the lines after JATOS starts should look like this (with your database URL).

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


### Uploading of study result files (JATOS >= v3.5.1)

1. Via `conf/production.conf`

   * `jatos.resultUploads.enabled` - Enables study result files uploads (default is true)
   * `jatos.resultUploads.path` - Path in the file system where the uploaded result files will be stored (default is './result_uploads')
   * `jatos.resultUploads.maxFileSize` - Max file size for one single uploaded result file (default is 30 MB)
   * `jatos.resultUploads.limitPerStudyRun` - Limit of all uploaded result files of one single study run (default is 50MB)

1. The path can be configured via environment variables

   ~~~bash
   export JATOS_RESULT_UPLOADS_PATH="/path/to/my/result/upload/folder"
   ~~~

1. The path can be configured via command-line arguments

   ~~~bash
   loader.sh start -DJATOS_RESULT_UPLOADS_PATH="/path/to/my/result/upload/folder"
   ~~~


### Study logs (since JATOS >= 3.2.1)

1. Via `conf/production.conf`

   * `jatos.studyLogs.enabled` - (since JATOS >= 3.5.1) - Enables [Study Logs](Study-Log.html) (default is true)
   * `jatos.studyLogs.path` - (since JATOS >= 3.2.1) - Path in the file system where the [Study Logs](Study-Log.html) will be stored (default is './study_logs')

1. The path can be configured via environment variables

   ~~~bash
   export JATOS_STUDY_LOGS_PATH="/path/to/my/study/logs/folder"
   ~~~

1. The path can be configured via command-line arguments

   ~~~bash
   loader.sh start -DJATOS_STUDY_LOGS_PATH="/path/to/my/study/logs/folder"
   ~~~


### LDAP authentication (since JATOS >= 3.5.4)

By default JATOS uses only locally stored users and no LDAP. LDAP configuration is only possible in `conf/production.conf`. At the moment LDAP users still have to be created manually in JATOS' user manager (with the checkbox LDAP turned on).- only authentication is done via LDAP.

* `jatos.user.authentication.ldap.url` - Specifies URL of the LDAP server. Not set or an empty string means no authentication via LDAP.
* `jatos.user.authentication.ldap.basedn` - LDAP base domain name (e.g. "dc=example,dc=com"). Not set or an empty string means no authentication via LDAP.
* `jatos.user.authentication.ldap.timeout` -  Time in milliseconds JATOS waits for a response from your LDAP server. Default is 5000 ms.

If your LDAP uses encryption, you have to add your certificate to JATOS' trusted certificates defined with `play.ws.ssl.trustManager.stores`. E.g. if your certificate's location is in `/jatos/conf/certs/ca.pem`, then use the following to add it: `play.ws.ssl.trustManager.stores = [ { type = "PEM", path = "/jatos/conf/certs/ca.pem" } ]`. 'type' can be PKCS12, JKS or PEM.


### User session configuration

The user session is part of JATOS secuity measurments ([more about security](http://blog.jatos.org/Hardening-JATOS-Security/)) and can be configured in `conf/production.conf`. 

* `jatos.userSession.validation` - (since JATOS >= 3.1.10) - toggles user session validation. If turned on (true) only the IP which was used at login time is allowed to be used for subsequent requests by this user. This helps preventing session hijacking and adds an addional layer of security. But on the downside it also prevents using the same user in JATOS from different browsers at the same time. By default it is set to false to allow an easy use of a local JATOS. On a server installation it should be set to true, although sometimes this not possible, e.g. if your users have an often changing, dynamic IP address. WARNING: Turning off the user session validation reduces JATOS security!

Other configs are:

* `jatos.userSession.timeout` - time in minutes a user stays logged in (default is 1440 = 1 day)
* `jatos.userSession.inactivity` - defines the time in minutes a user is automatically logged out after inactivity (default is 60)


### Other configuration in production.conf

Some other properties can be configured in the `conf/production.conf`.

* `play.http.session.secure` - secure session cookie: set true to restrict user access to HTTPS (default is false)

Apart from those all [configuration properties possible in the Play Framework](https://www.playframework.com/documentation/latest/Configuration) are possible in JATOS production.conf too, e.g. 
* `pidfile.path` - Path to the file that contains the process id of the started JATOS application (default is ./RUNNING_PID) 


