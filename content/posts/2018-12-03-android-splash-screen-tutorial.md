+++
categories = ["android"]
date = "2021-04-04"
description = "Android splash screen that shows for minimal time without wasting user time and works on all android versions including oreo and above"
title = "Android Splash Screen Tutorial"
+++

Android splash screen is important when your app takes time to open, it is not required on all apps but it is need when app needs to make network request or do some processor intensive taks, anyways who cares about that. We are going to implement splash screen that shows on a cold app launch but will be non existent on a hot launch. Let's code. Create a new Android project and create a new activity `SplashActivity`.

## Steps

We are going to do it in following steps
- Create Android Project.
- Create `SplashActivity`.
- Create a drawable.
- Create a theme in styles.


## Creating Drawable

Create a new file in `res/drawable`
Name it `splash_background` or something else.
I am going to use `splash_background` in this example

TODO: Line 18 - Replace app_logo with your logo <br>	
TODO: Line 8, 9 & 10 - Change colors according to your app logo

```xml
<?xml version="1.0" encoding="utf-8"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">
<item>
        <shape xmlns:android="http://schemas.android.com/apk/res/android"
            android:shape="rectangle" >
            <gradient
                android:angle="90"
                android:centerColor="#2f3640"
                android:endColor="#353b48"
                android:startColor="#2f3640" />
        </shape>
    </item>

    <item>
        <bitmap
            android:id="@+id/logo"
            android:gravity="center"
            android:src="@drawable/app_logo" />
    </item>

</layer-list>
```
## Creating A New Theme

Navigate to `styles.xml` and add a new theme for splash activity

```xml
<resources>

    ...

    <style name="SplashTheme" parent="Theme.AppCompat.NoActionBar">
        <item name="android:windowBackground">@drawable/splash_background</item>
    </style>

</resources>
```

For API level 26 and above add on line 6

```xml
<item name="android:windowSplashscreenContent">@drawable/splashscreen</item>
```

## Configure SplashActivity's Theme

```xml
<activity
    android:name=".SplashActivity"
    android:theme="@style/SplashTheme">
    <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
</activity>
```

## Finally Lanuch MainActivity from SplashActivity

```java
public class SplashActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        Intent intent = new Intent(this, MainActivity.class);
        startActivity(intent);
        finish();
    }
}
```
