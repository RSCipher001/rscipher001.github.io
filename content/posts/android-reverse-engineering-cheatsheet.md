---
title: "Android Reverse Engineering Cheatsheet"
date: 2019-11-10T23:33:00+05:30
description: "Android Reverse Engineering Cheatsheet"
tags: [android, infosec, apk, adb]
category: [Android]
---

Some resources and references for reverse engineering APKs

## Static Analysis
Static analysis is really important, there are many tools out there for the job but I like StaCoAn. It is really awesome

## ADB
ADB is really powerful and can be very useful when reverse engineering APK. Here is the list of commands that can be useful in extracting data from APKs

```bash
adb logcat # Too verbose always filter data with grep
```

```bash
string apk_file # Too verbose try filtering with grep
```