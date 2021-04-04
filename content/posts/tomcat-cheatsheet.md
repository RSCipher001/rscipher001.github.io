---
title: "Tomcat Cheatsheet"
date: 2020-01-01T00:11:28+05:30
description: "Ubuntu tomcat installation and setup"
tags: [tomcat]
---

## Installation
```bash
sudo apt install openjdk-8-jdk tomcat9 tomcat9-admin tomcat9-user tomcat9-examples tomcat9-docs 
# mysql-server
```


## Create a new tomcat user
```bash
cd /var/lib/tomcat9/conf
vim tomcat-users.xml
```

Append these at the end of `tomcat-users.xml`
```xml
<role rolename="manager-gui"/>
<role rolename="manager-script"/>
<role rolename="manager-jmx"/>
<role rolename="manager-status"/>
<user username="admin" password="STRONG_PASSWORD" roles="admin-gui, manager-gui, manager-script, manager-jmx, manager-status"/>
<user username="deployer" password="STRONG_PASSWORD" roles="manager-script"/>
<user username="tomcat" password="STRONG_PASSWORD" roles="manager-gui"/>
```

## Increase upload size from 50MB to 500MB
```bash
vim /usr/share/tomcat9-admin/manager/WEB-INF/web.xml
# And update size of multipart option
```
## Change port from 8080 to 80
```bash
vim /var/lib/tomcat9/conf/server.xml
# And change port from 8080 to 80
```