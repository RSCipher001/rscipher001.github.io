---
title: "Sublist3r Cheatsheet"
date: 2019-11-17T19:46:00+05:30
description: "Sublist3r Cheatsheet"
tags: [Sublist3r]
---

Some of the most used options of sublist3r

## Installation
Clone from git

```bash
git clone https://github.com/aboul3la/Sublist3r.git
```

## Scan a domain for subdomains

```bash
python3 sublist3r.py -d example.com
```

### Options
```bash
-b Bruteforce
# Warning:			Scan takes long time but finds more subdomains than regular scan
# Recommendation:	Use it

-p Scan found domains for specified ports
# Warning			Scan takes much longer
# Recommendation	Depends on your setup

-v Verbose
# Recommendation	Use it

-o Output file
# Recommendation	Always use it

-n Colorless Output
# Recommendation	Depends
```

### Example

```bash
python3 sublist3r.py -d example.com -b -v -n -o example.com
```