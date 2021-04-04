+++
categories = ["android"]
date = "2021-04-04"
description = "In this post we will see that how to check whether a host reachable or not in Android by using ping command programatically."
title = "Android How to Ping a Server Programatically"
+++

Finding a solution in Android is never easy, sometimes you find a solution but it is using deprecated libraries or it won't work on all Android versions, etc. That's why I am relying on an external binary called `ping`. Ping is avaiable in all android phones and it is very mature.

## Steps
- Create Android Project
- Add Internet Permission
- Ping A Server
- Check Result

## Code

```java
import android.content.Context;
import android.net.ConnectivityManager;
import android.net.NetworkInfo;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.util.Log;
import android.widget.Toast;

import java.io.IOException;
import java.net.InetAddress;

public class MainActivity extends AppCompatActivity {

    Boolean isConnected = false,
            isWiFi = false,
            isMobile = false;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // https://developer.android.com/training/monitoring-device-state/connectivity-monitoring
        ConnectivityManager cm =
                (ConnectivityManager) this.getSystemService(Context.CONNECTIVITY_SERVICE);

        NetworkInfo activeNetwork = cm.getActiveNetworkInfo();

        // True if network is available.
        if (activeNetwork != null) {

            // True if using WiFI
            isWiFi = activeNetwork.getType() == ConnectivityManager.TYPE_WIFI;

            // True if using Mobile Data
            isMobile = activeNetwork.getType() == ConnectivityManager.TYPE_MOBILE;

            isConnected = activeNetwork.isConnectedOrConnecting();
        }

        if (isConnected) {
            if (isWiFi) {
                Toast.makeText(this, "Yes, WiF", Toast.LENGTH_SHORT)
                        .show();

                // ping google server for testing purpose
                if (isConnectedToThisServer("www.google.com")) {
                    Toast.makeText(this, "Yes, Connected to Google", Toast.LENGTH_SHORT)
                            .show();
                } else {
                    Toast.makeText(this, "No Google Connection", Toast.LENGTH_SHORT)
                            .show();
                }
            }


            if (isMobile) {

                Toast.makeText(this, "Yes, Mobile", Toast.LENGTH_SHORT)
                        .show();
                if (isConnectedToThisServer("www.google.com")) {
                    Toast.makeText(this, "Yes, Connected to Google", Toast.LENGTH_SHORT).show();
                } else {
                    Toast.makeText(this, "No Google Connection", Toast.LENGTH_SHORT).show();
                }
            }
        } else {
            Toast.makeText(this, "No Network", Toast.LENGTH_SHORT).show();
        }
    }


    // Function that uses ping, takes server name or ip as argument.
    public boolean isConnectedToThisServer(String host) {
        // https://stackoverflow.com/questions/3905358/how-to-ping-external-ip-from-java-android
        Runtime runtime = Runtime.getRuntime();
        try {
            Process ipProcess = runtime.exec("/system/bin/ping -c 1 " + host);
            int exitValue = ipProcess.waitFor();
            return (exitValue == 0);
        } catch (IOException e) {
            e.printStackTrace();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        return false;
    }
}
```