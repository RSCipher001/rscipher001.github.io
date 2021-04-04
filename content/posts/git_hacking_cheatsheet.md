+++
categories = ["infosec"]
date = "2021-04-04"
description = "Git Hacking"
title = "Git Hacking"
+++

Git is my favorite tool when developing software, it make our job so easy because it maintains past versions of our file and branches makes it easy to work on different features at the same time. Git stores data in .git folder and this folder is contains many files, The following is list of tools and notes that can help you with retriving real code from `.git` folder, It is a combination of common git commands and avaiable tools on the internet.

# Retrive All Code From .git Folder
```bash
git reset HEAD --hard
# It will remove modified files from current folder
```

# List All Files That is being tracked by git
```bash
git ls-files
# This information is stored in .git/index and this file can be downloaded for many website that can help you with recon stat and it can be used to find juicy information
```