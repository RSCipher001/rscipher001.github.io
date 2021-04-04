---
title: "Firebase Cheatsheet"
date: 2019-11-10T00:23:08+05:30
description: "Firebase Cheatsheet is a great way to sneak peak FCM related stuff without going through documentation"
tags: [firebase]
---


### Trigger notification using CURL
```bash
curl -X POST --header "Authorization: key=AIzaSyA7ysOSRMqiv2hiWHJmai1yXiTLhP4oztMz" \
	--Header "Content-Type: application/json" \
	https://fcm.googleapis.com/fcm/send \
	-d "{\"to\":\"fB95hP9NZJ8:APA91bFwORxZm08noNx6yEJu0kg97P5957P8zyP0NKmvUyExW1OlfUAVaPuX9gEC-BAkl_fi2HJshZj5WN4KNvDiR8B0Oug6oKy2boLoCC_EYOA0oeZvAdc_rLo9yLsyXy2bCp4jurJiz\",\"notification\":{\"body\":\"ENTER YOUR MESSAGE HERE\"}"
```

Replace `key=AIzaSyA7ysOSRMqiv2hiWHJmai1yXiTLhP4oztMz` with your own key, You can create keys in Firebase Console.

Replace `fB95hP9NZJ8:APA91bFwORxZm08noNx6yEJu0kg97P5957P8zyP0NKmvUyExW1OlfUAVaPuX9gEC-BAkl_fi2HJshZj5WN4KNvDiR8B0Oug6oKy2boLoCC_EYOA0oeZvAdc_rLo9yLsyXy2bCp4jurJiz` with device FCM token.

### Check Firestore security
Make a get request to `project-name.firebaseio.com/.json`.