+++
categories = ["android", "adb"]
date = "2021-04-04"
description = "How to remove preinstalled Android bloatware without root using adb"
title = "Remove Bloatware Without Root in Android"
+++

If you want to remove preinstalled from your Android phone then this post is for you.

## Requirements
- An Android
  - USB Debugging should be on.
- A Computer (Mac, Linux or Windows)
  - ADB should be installed.
  - ADB drivers should be installed (Windows only)

ADB Downloads: https://developer.android.com/studio/releases/platform-tools

## Staging
- Connect your phone with your computer and make sure adb is working by typing `adb devices -l`, it will show a prompt in your phone, accept it, run `adb devices -l` again and it should output your phone model/codename in terminal.
- In many phones you have to select connection type as MTP or they won't work.


## Let's remove Facebook.

To remove apps from phone using ADB we need to know it's package name, let's remove Facebook, open Google and search `facebook play store` and click on first link which should be `https://play.google.com/store/apps/details?id=com.facebook.katana&hl=en_US`, you can see id=`com.facebook.katana` that's package name for facebook, you can find package name by any other method too it doesn't matter as long as it is correct.

Open your terminal and type `adb shell pm uninstall --user 0 com.facebook.katana` and it will remove facebook for current user, if you have more than one user then you have to change `--user 0` to `--user x`.

List All Users

```bash
$ adb shell pm list users
Users:
      UserInfo{0:Ravindra:13} running
      UserInfo{10:Test:10} running
```

User id is: 0 in UserInfo{`0`:Ravindra:13} running
User id is: 10 in UserInfo{`10`:Test:10} running

To remove Facebook for user Test with id 10 run
```bash
adb shell pm uninstall --user 10 com.facebook.katana
```
