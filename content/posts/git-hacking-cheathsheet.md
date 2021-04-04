---
title: "Git Hacking Cheatsheet"
date: 2019-11-10T23:33:00+05:30
description: "Recon Cheatsheet"
tags: [infosec, hacking, ethical hacking, sublister, nmap]
---

Git is my favorite tool when developing software, it make our job so easy because it maintains past versions of our file and branches makes it easy to work on different features at the same time. Git stores data in .git folder and this folder contains many files, The following is list of tools and notes that can help you with retriving real code from `.git` folder, It is a combination of common git commands and avaiable tools on the internet.

## Retrive All Code From .git Folder
```bash
git reset HEAD --hard
# It will remove modified files from current folder
```

## List All Files That is being tracked by git
```bash
git ls-files
# This information is stored in .git/index and this file can be downloaded for many website that can help you with recon stat and it can be used to find juicy information
```

Git store list of files in `.git/index`, this file can be used to list all files being tracked by git.
If you can download .git/index of a website then you can get a list of all files before running programs like GitTools.

### Steps
- Create an empty folder and cd into it.
- Create an empty .git repositoy by typing `git init`.
- Create an empty file by typing `touch file`.
- Add file to git by typing `git add file`.
- Now go to `.git` and replace existing `index` with downloaded `index`.
- Now type `cd ..` to come back to our new folder.
- Now type `git ls-files` to list all files.