---
title: "Java Spring Cheatsheet"
date: 2019-11-21T09:49:00+05:30
description: "Spring Cheatsheet contains a very few things I know about spring boot and spring mvc"
tags: [java, spring, springboot, springmvc]
---

# Enable Session Time Zone when running SQL queries

This is really usefull when you're using now() in mysql to set time in table
```java
// For IST
value="jdbc:mysql://localhost:3306/dbname?serverTimezone=+5:30"

// For UTC
value="jdbc:mysql://localhost:3306/dbname?serverTimezone=UTC"
```

