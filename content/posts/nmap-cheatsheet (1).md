---
title: "NMap Cheatsheet"
date: 2019-11-10T23:16:00+05:30
description: "Some Common Nmap commands"
tags: [mysql]
---

### Scan a Host
```bash
nmap <host>
```

```bash
nmap localhost
```

**Note: You can use IP or website as hostname**

### Scan a range of IP
```bash
nmap 192.168.43.1-100
```

### Scan a subnet
```bash
nmap 192.168.43.1.0/24
```

### Scan targets from a file
```bash
nmap -iL <filename>
```

### Save result to a file
```
nmap -oA <filename>
```

### Convert XML output file to HTML
```bash
xsltproc <nmap-output.xml> -o <nmap-output.html>
```

### Enable service version detection
```bash
nmap -sV <host>
```

### Specify Port Number
```bash
nmap -p80 <host>
```

### Fingerprint WAF
```bash
nmap --script=http-waf-fingerprint <host>
```

### Fingerprint WAF (Intensive)
```bash
nmap --script=http-waf-fingerprint --script-args http-waf-fingerprint.intensive=1 <host>
```

./masscan -p- 89.16.163.96/28 -–rate=10000
./masscan -p80,8000-8100 10.0.0.0/8 --rate=10000
