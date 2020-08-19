---
title: JATOS with Nginx
keywords: nginx, server, installation, encryption, HTTPS
tags:
summary:
sidebar: mydoc_sidebar
permalink: JATOS-with-Nginx.html
folder:
toc: true
last_updated: 19 Aug 2020
---

These are examples for configurations of [Nginx](https://www.nginx.com/) as a proxy in front of JATOS. It is not necessary to run JATOS with a proxy but it's common. They support WebSockets for JATOS' group studies. 

The following two configs are the content of `/etc/nginx/nginx.conf`. Change them to your needs. You probably want to change your servers address (`www.example.com` in the example) and the path to the SSL certificate and its key. This `proxy_set_header X-Forwarded-*` is necessary to tell JATOS the original requester's IP address - please leave it unchanged.

As an additional security measurement you can uncomment the `location /jatos` and config your local network. This will restrict the access to JATOS' GUI (every URL starting with `/jatos`) to the local network.

A JATOS server that handles sensitive or private data should always use encryption (HTTPS).

## With HTTPS

~~~ shell
user www-data;
worker_processes auto;
pid /run/nginx.pid;

events {
        worker_connections 768;
        # multi_accept on;
}

http {
        sendfile on;
        keepalive_timeout 65;
        client_max_body_size 500M;

        include /etc/nginx/mime.types;
        default_type application/octet-stream;

        proxy_buffering    off;
        proxy_set_header   X-Forwarded-Proto https;
        proxy_set_header   X-Forwarded-Ssl on;
        proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header   Host $http_host;
        proxy_http_version 1.1;

        upstream jatos-backend {
                server 127.0.0.1:9000;
        }

        # needed for websockets
        map $http_upgrade $connection_upgrade {
                default upgrade;
                ''      close;
        }

        # redirect http to https
        server {
                listen       80;
                server_name www.example.com;
                rewrite ^ https://www.example.com$request_uri? permanent;
        }

        server {
                listen               443;
                ssl                  on;

                # http://www.selfsignedcertificate.com/ is useful for development testing
                ssl_certificate      /etc/ssl/certs/localhost.crt;
                ssl_certificate_key  /etc/ssl/private/localhost.key;

                # From https://bettercrypto.org/static/applied-crypto-hardening.pdf
                ssl_prefer_server_ciphers on;
                ssl_protocols TLSv1 TLSv1.1 TLSv1.2; # not possible to do exclusive
                ssl_ciphers 'EDH+CAMELLIA:EDH+aRSA:EECDH+aRSA+AESGCM:EECDH+aRSA+SHA384:EECDH+aRSA+SHA256:EECDH:+CAMELLIA256:+AES256:+CAMELLIA128:+AES128:+SSLv3:!aNULL:!eNULL:!LOW:!3DES:!MD5:!EXP:!PSK:!DSS:!RC4:!SEED:!ECDSA:CAMELLIA256-SHA:AES256-SHA:CAMELLIA128-SHA:AES128-SHA';
                add_header Strict-Transport-Security "max-age=15768000; includeSubDomains";

                keepalive_timeout    70;
                server_name www.example.com;

                # websocket location (JATOS' group and batch channel and the test page)
                location ~ "/(jatos/testWebSocket|publix/[\d]+/(group/join|batch/open))" {
                        proxy_pass              http://jatos-backend;
                        proxy_http_version      1.1;
                        proxy_set_header        Upgrade $http_upgrade;
                        proxy_set_header        Connection $connection_upgrade;
                        proxy_connect_timeout   7d; # keep open for 7 days even without any transmission
                        proxy_send_timeout      7d;
                        proxy_read_timeout      7d;
                }

                # restrict access to JATOS' GUI to local network
                #location /jatos {
                #       allow           192.168.1.0/24;
                #       deny            all;
                #       proxy_pass      http://jatos-backend;
                #}

                # all other traffic
                location / {
                        proxy_pass              http://jatos-backend;
                }
        }

        access_log /var/log/nginx/access.log;
        error_log /var/log/nginx/error.log;

        include /etc/nginx/conf.d/*.conf;
        #include /etc/nginx/sites-enabled/*;
}
~~~


## With HTTPS and Docker

Have a look at [github.com/robinsonkwame/jatos-https-docker-compose](https://github.com/robinsonkwame/jatos-https-docker-compose) for a good example in how to do this (Thanks to Kwame Porter Robinson)


## Simple without encryption

~~~ shell
user www-data;
worker_processes auto;
pid /run/nginx.pid;

events {
        worker_connections 768;
        # multi_accept on;
}

http {
        sendfile on;
        keepalive_timeout 65;
        client_max_body_size 500M;

        include /etc/nginx/mime.types;
        default_type application/octet-stream;

        proxy_buffering    off;
        proxy_set_header   X-Forwarded-Proto http;
        proxy_set_header   X-Forwarded-Ssl on;
        proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header   Host $http_host;
        proxy_http_version 1.1;

        upstream jatos-backend {
                server 127.0.0.1:9000;
        }

        # needed for websockets
        map $http_upgrade $connection_upgrade {
                default upgrade;
                ''      close;
        }

        server {
                listen               80;

                keepalive_timeout    70;
                server_name          www.example.com;

                # websocket location (JATOS' group and batch channel and the test page)
                location ~ "^/(jatos/testWebSocket|publix/[\d]+/(group/join|batch/open))" {
                        proxy_pass              http://jatos-backend;
                        proxy_http_version      1.1;
                        proxy_set_header        Upgrade $http_upgrade;
                        proxy_set_header        Connection $connection_upgrade;
                        proxy_connect_timeout   7d; # keep open for 7 days even without any transmission
                        proxy_send_timeout      7d;
                        proxy_read_timeout      7d;
                }

                # restrict access to JATOS' GUI to local network
                #location /jatos {
                #       allow           192.168.1.0/24;
                #       deny            all;
                #       proxy_pass      http://jatos-backend;
                #}

                # all other traffic
                location / {
                        proxy_pass              http://jatos-backend;
                }
        }

        access_log /var/log/nginx/access.log;
        error_log /var/log/nginx/error.log;

        include /etc/nginx/conf.d/*.conf;
        #include /etc/nginx/sites-enabled/*;
}
~~~
