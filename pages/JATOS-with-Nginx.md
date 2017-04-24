---
title: JATOS with Nginx
keywords: nginx, server, installation
tags:
summary:
sidebar: mydoc_sidebar
permalink: JATOS-with-Nginx.html
folder:
toc: true
last_updated: 29 Dec 2016
---

This is an example for a configuration of [Nginx](https://www.nginx.com/) as a proxy in front of JATOS. It is not necessary to run JATOS with a proxy but it's common. It supports encryption (HTTPS) and WebSockets for JATOS' group studies. 

The following is the content of `/etc/nginx/nginx.conf`. Change it to your needs. You probably want to change your servers address (`www.example.com` in the example) and the path to the SSL certificate and its key.

~~~ shell
user www-data;
worker_processes 1;
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
        proxy_set_header   X-Real-IP $remote_addr;
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

                # websocket location (JATOS' group channel)
                location ~ "^/publix/[\d]+/group/join" {
                        proxy_pass              http://jatos-backend;
                        proxy_set_header        Upgrade $http_upgrade;
                        proxy_set_header        Connection $connection_upgrade;
                        proxy_read_timeout      3600; # keep open even without any transmission
                }

                # all other traffic
                location / {
                        proxy_pass              http://jatos-backend;
                }
        }

        access_log /var/log/nginx/access.log;
        error_log /var/log/nginx/error.log;

        include /etc/nginx/conf.d/*.conf;
        include /etc/nginx/sites-enabled/*;
}
~~~
