---
title: "htaccess Cheatsheet"
date: 2019-11-10T00:23:08+05:30
description: "Some very common htaccess usage"
tags: [apache, htaccess]
---

.htaccess is a hidden file that is mostly used with Apache servers to override apache settings, It can be used for many purposes writing something in it is equivalent to writing in `apache.ini`. Following is list of apache configs that I use regularly to accomplish common tasks.


# Enforce HTTPS
```
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```