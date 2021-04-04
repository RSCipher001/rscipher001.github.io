+++
categories = ["apache", "htaccess"]
date = "2021-04-04"
description = "HTaccess Cheatsheet"
title = "HTaccess Cheatsheet"
+++

.htaccess is a hidden file that is mostly used with Apache servers to override apache settings, It can be used for many purposes writing something in it is equivalent to writing in `apache.ini`. Following is list of apache configs that I use regularly to accomplish common tasks.


# Enforce HTTPS
```
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```