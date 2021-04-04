+++
categories = ["devops", "sysadmin"]
date = "2021-04-04"
description = "Apache server cheatsheet contains list of commonly used apache config and settings to help you with setting up a server"
title = "Apache server Cheatsheet"
+++

Prevent access to all files starting with `.` (dot). This will help us protect files like .htaccess, .env and folders like .git, .svn, .trash, etc.

```
<FilesMatch "^\.">
    Order allow,deny
    Deny from all
</FilesMatch>
```
