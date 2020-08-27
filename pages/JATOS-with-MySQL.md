---
title: JATOS with MySQL
keywords: server, installation, MySQL, database
tags:
summary: 
sidebar: mydoc_sidebar
permalink: JATOS-with-MySQL.html
folder:
toc: true
last_updated: 26 Aug 2020
---

By default JATOS uses an embedded H2 database and no further setup is necessary but it can be easily configured to work with a MySQL database.

Possible scenarios why one would use an external database are
* your JATOS will be used by more than a few users (e.g. several research groups or an institute-wide installation)
* your JATOS will run studies with many participants
* the expected traffic is rather high (the studies produce a lot of result data)
* you want to be able to do a regular database backup (with the embedded H2 database this would involve stopping JATOS)
* higher trust in the reliability of MySQL (although we had no problems with H2 so far)

## Installation

One could install the external database on the same server as JATOS is running or on an extra server depending on ones need.

There are many manuals out there, e.g. [this one](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04). One way to set up MySQL:
   
   1. Install MySQL, e.g. on Ubuntu

      **JATOS requires MySQL >= 5.7 (8.x is fine)**

      ```bash
      sudo apt install mysql-server
      ```
   
   1. Log in to MySQL's command line terminal:

      ```bash
      mysql -u root -p
      ```
   
   1. Create a user for JATOS: 
   
      You can use any username and password but have to remember them when configuring JATOS later on.

      ```bash
      GRANT ALL PRIVILEGES ON *.* TO 'jatosuser'@'localhost' IDENTIFIED BY 'password';
      ```
   
   1. Log out and log in with the newly created user:
   
      ```bash
      mysql -u jatosuser -p
      ```
   
   1. Create a database for JATOS:

      **Character set and collation are important - otherwise you won't have full UTF-8 support**
   
      ```bash
      CREATE DATABASE jatos CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
      ```
   
   1. Exit the database with `exit`

Appart from giving JATOS access to the database it is **not** necessary to create any tables - JATOS is doing this automatically.

Now you have to configure JATOS to use your MySQL.


## Configure JATOS

There are three ways to set up JATOS to work with a MySQL database. If you are in doubt use 'production.conf'.

1. Via JATOS config file which is in your JATOS folder in the `conf` folder: `conf/production.conf`

   Change IP, port, username and password to your needs.

   ~~~ bash
   db.default.url="jdbc:mysql://127.0.0.1:3306/jatos?characterEncoding=UTF-8&useJDBCCompliantTimezoneShift=true&useLegacyDatetimeCode=false&serverTimezone=UTC"
   db.default.user="jatosuser"
   db.default.password="mypassword"
   db.default.driver=com.mysql.cj.jdbc.Driver
   ~~~

   **Always restart JATOS after making any changes to the configuration (e.g. with `./loader.sh restart`)**

1. Via command-line arguments:
   * `-DJATOS_DB_URL` - specifies the URL to the database
   * `-DJATOS_DB_USERNAME` - set your username
   * `-DJATOS_DB_PASSWORD` - set your password
   * `-DJATOS_DB_DRIVER` - always `com.mysql.cj.jdbc.Driver` for MySQL
   
   E.g. to connect to a MySQL running on 127.0.0.1 and port 3306 use (but change username and password):
   
   ~~~ bash   
   loader.sh start -DJATOS_DB_URL='jdbc:mysql://127.0.0.1:3306/jatos?characterEncoding=UTF-8&useJDBCCompliantTimezoneShift=true&useLegacyDatetimeCode=false&serverTimezone=UTC' -DJATOS_DB_USERNAME=sa -DJATOS_DB_PASSWORD=sa -DJATOS_DB_DRIVER=com.mysql.cj.jdbc.Driver
   ~~~
   
1. Via environment variables (change IP, port, username and password)

   ~~~ bash
   export JATOS_DB_URL="jdbc:mysql://127.0.0.1:3306/jatos?characterEncoding=UTF-8&useJDBCCompliantTimezoneShift=true&useLegacyDatetimeCode=false&serverTimezone=UTC"
   export JATOS_DB_USERNAME=jatosuser
   export JATOS_DB_PASSWORD='mypassword'
   export JATOS_DB_DRIVER=com.mysql.cj.jdbc.Driver
   ~~~

You can confirm that JATOS is accessing the correct database by looking in the logs. One of the lines after JATOS starts should look like this (with your database URI):

~~~ bash
14:06:01.760 [info] - p.a.d.DefaultDBApi - Database [default] initialized at jdbc:mysql://localhost/jatos?characterEncoding=UTF-8&useJDBCCompliantTimezoneShift=true&useLegacyDatetimeCode=false&serverTimezone=UTC
~~~

Done. Your JATOS uses your MySQL now.


## [Optional] Deactivate MySQL's binary log

MySQL's binary logs (also called binlogs) serve two purposes: replication and data recovery. More can be found in [MySQLs documentation](https://dev.mysql.com/doc/internals/en/binary-log-overview.html#:~:text=The%20binary%20log%20is%20a,14.).

The problem with binary logs is that they can take up quite some disk space depending on the experiments you run on your JATOS. If you have a single MySQL instance (and therefore do not use replication) and you do not need MySQL's data recovery (e.g. have a different backup mechanism) than it is safe to deactivate the binary logs. 

### Via MySQL config

Add `skip-log-bin` to the end of your MySQL config. On many Linux systems the config is in `/etc/mysql/mysql.conf.d/mysqld.cnf`.

The part of your 'mysqld.cnf' that configures the binary logs could then look similar to this:

```bash
# The following can be used as easy to replay backup logs or for replication.
# note: if you are setting up a replication slave, see README.Debian about
#       other settings you may need to change.
# server-id             = 1
# log_bin                       = /var/log/mysql/mysql-bin.log
# binlog_expire_logs_seconds    = 2592000
# max_binlog_size   = 100M
# binlog_do_db          = include_database_name
# binlog_ignore_db      = include_database_name
skip-log-bin
```

You have to restart MySQL for the changes to take effect.

### Via MySQL global variable

If your MySQL is already running and you don't want to restart it, there is a way to turn off the binary logging with a [global variable](https://dev.mysql.com/doc/refman/8.0/en/replication-options-binary-log.html#option_mysqld_log-bin):

Log into your MySQL console and type:

1. Log in to MySQL's command line terminal:

   ```bash
   mysql -u root -p
   ```

1. Set 'sql_log_bin'

   ```bash
   SET sql_log_bin = OFF;
   ```

This is reversible by setting it to `ON`.
