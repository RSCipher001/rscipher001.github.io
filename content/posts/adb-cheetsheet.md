+++
categories = ["android", "adb"]
date = "2021-04-04"
description = "ADB Cheatsheet that includes most commonly used adb commands"
title = "ADB Cheathsheet"
+++

A list of ADB Commands

### List all connected devices
```bash
adb list devices
adb list devices -l # Long Output
```

### Enable Wireless ADB on a USB Connected Device
```bash
adb tcpip 5555  # 5555 is port, can be changed if needed
```

### adb connect using device IP
```bash
adb connect 192.168.43.1:5555 # 5555 is Port
```

### ADB Port Forward
```bash
adb forward tcp:808 tcp:8080 # Typing localhost on computer will access mobile server at port 8080

adb forward --remove tcp:8080 # Remove specific forward
adb forward --remove-all # Remove All Port Forwarding
```

### ADB Port Reverse
```bash
adb reverse tcp:808 tcp:8080 # Typing localhost on mobile will access computer server at port 8080

adb reverse --remove tcp:8080 # Remove specific reverse
adb reverse --remove-all # Remove All Port reversing
```
### List All Installed Packages
```bash
adb shell cmd package list package
adb shell cmd package list package -f # Full Information
```

### Remove bloatware
```bash
adb shell pm uninstall --user 0 `package.name`
# Replace package name with your application package name.
# Ex: Package name for WhatsApp: com.whatsapp
```

### Check Multi user Support
```bash
adb shell pm list max-users # Outputs more than one on multi-user support
```

### Set/Hack Multi-user Support
```bash
adb shell setprop fw.max_users = 5
# This will temporarily set max user value to 5 and new user can be created on unsupported phones
```

### Misc
```bash
adb shell "dumpsys package | grep -A1 'userId=UID'"
# I think it is used for getting app name from PID.
```

