+++
categories = ["infosec", "nmap"]
date = "2021-04-04"
description = "NMap Cheatsheet"
title = "NMap Cheatsheet"
+++

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