+++
categories = ["infosec"]
date = "2021-04-04"
description = "Android Reverse Engineering Cheatsheet"
title = "Android Reverse Engineering Cheatsheet"
+++

Android is the most famous platform in the world so security is really import for Android devices, Google provides a lot of resources for Android Security but developers still make mistakes, here is the list of tools and commands to extract juicy information from Android Applications.

# Static Analysis
Static analysis is really important, there are many tools out there for the job but I like StaCoAn. It is really awesome

# ADB
ADB is really powerfull and can be very usefull when reverse engineering APK. Here is the list of commands that can be usefull in extracting data from APKs

```bash
adb logcat # Too verbose always filter data with grep
```

```bash
string apk_file # Too verbose try filtering with grep
```