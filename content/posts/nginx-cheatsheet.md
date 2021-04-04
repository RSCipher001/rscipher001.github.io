---
title: "Nginx cheatsheet"
date: 2019-12-21T11:24:00+05:30
description: "Nginx cheatsheet conatins usefull references related to nginx server configuration"
tags: [nginx, sysadmin, server, ssl]
---

This page contains some of the very usefull nginx stuff I always use

## Config for a static website
```
server {
    add_header Strict-Transport-Security "max-age=31536000; includeSubDomains; preload" always;

    # Listen
    listen 80; 
    listen [::]:80;

    # Redirect
    if ($host = notes.ravindrasecureserver.online) {
        return 301 https://$host$request_uri;
    }   

    # Project
    server_name notes.ravindrasecureserver.online;
    return 404;
}

server {
    # Listen
    listen 443 ssl http2;
    listen [::]:443 ssl http2 ipv6only=on;

    # Headers
    add_header Strict-Transport-Security "max-age=31536000; includeSubDomains; preload" always;
    add_header Referrer-Policy "strict-origin-when-cross-origin";
    add_header Feature-Policy "geolocation 'none'; vibrate 'none'; microphone 'none'; camera 'none'";
    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-XSS-Protection "1; mode=block";
    add_header X-Content-Type-Options "nosniff";
    add_header Content-Security-Policy "default-src 'self' https://fonts.googleapis.com https://fonts.gstatic.com; img-src 'self' data:; media-src 'self'; script-src 'self'";

    # Compression
    gzip on; 
    gzip_types application/javascript image/* text/css;
    gunzip on; 

    # Other
    charset utf-8;
    index index.html index.htm;

    # Project
    root /home/ubuntu/Projects/DaliyNotes
    server_name notes.ravindrasecureserver.online;

    # Location
    location ~ /\.(?!well-known).* {
        deny all;
    }   
    location = /favicon.ico {
        access_log off; log_not_found off;
    }   
    location = /robots.txt {
        access_log off; log_not_found off;
    }   


    # SSL 
    ssl_certificate /etc/letsencrypt/live/notes.ravindrasecureserver.online/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/notes.ravindrasecureserver.online/privkey.pem;
    include /etc/letsencrypt/options-ssl-nginx.conf;
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;
}
```