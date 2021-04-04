---
title: "React Native Cheatsheet"
date: 2019-11-10T23:30:00+05:30
description: "React Native Cheatsheet"
tags: [react, react native]
---

This is a under development kind of thing for react native concept I have been learning.

### Prepare your environment
First you need to install react-native cli, to do that use `sudo npm install -g react-native-cli` and installed JDK, Android SDK and set environment variables and PATH. For more info go to `https://facebook.github.io/react-native/docs/getting-started` and install yarn for faster node packages installation.

### Create your first react native app
Open Terminal and type
```bash
react-native init HelloWorld	# It will create a new folder named HelloWorld.
cd HelloWorld
react-native run-android 		# Run you app, May take some time for first run.
```
and connect your Android device to your computer.

# Generating Signed APK.
Refer `https://facebook.github.io/react-native/docs/signed-apk-android`