---
layout: post
title: "Using the Android AlarmManager with WorkManager for scheduled tasks in Flutter"
description: " "
date: 2023-10-01
tags: [Android]
comments: true
share: true
---

In Flutter, there may be times when you need to schedule tasks to be executed at a specific time or at regular intervals. While Flutter provides the `Timer` class for basic scheduling, it is limited and not suitable for tasks that need to survive app restarts or device reboots. In such cases, using the Android `AlarmManager` with `WorkManager` can be an effective solution. 

## What is AlarmManager?

`AlarmManager` is an Android system service that allows you to schedule tasks to be executed at a given time or at regular intervals, even if your app is not running. It is ideal for scenarios such as reminder notifications, periodic data syncing, or alarm clock apps.

## What is WorkManager?

`WorkManager` is an Android library that makes it easy to schedule deferrable, asynchronous tasks that are expected to run even if the app process is killed or the device is restarted. It provides a simplified API for handling tasks in the background, ensuring that they are executed in a battery-efficient manner.

## Using AlarmManager with WorkManager in Flutter

To use `AlarmManager` with `WorkManager` in a Flutter app, you'll need to leverage the power of platform-specific code. Here's a step-by-step guide:

1. Create a new Flutter project.

2. Implement the Android-specific logic using Java or Kotlin:

```java
// Create a new BroadcastReceiver to receive the alarm broadcast
public class AlarmReceiver extends BroadcastReceiver {
    
    @Override
    public void onReceive(Context context, Intent intent) {
        // Create a WorkRequest to schedule the desired task
        OneTimeWorkRequest workRequest = new OneTimeWorkRequest.Builder(YourWorker.class)
                .build();

        // Enqueue the WorkRequest to be executed by WorkManager
        WorkManager.getInstance(context).enqueue(workRequest);
    }
}
```

3. Register the `AlarmReceiver` in the AndroidManifest.xml file:

```xml
<receiver android:name=".AlarmReceiver" />
```

4. Implement the `YourWorker` class that extends `Worker` and contains the actual task logic:

```java
public class YourWorker extends Worker {

    @NonNull
    @Override
    public Result doWork() {
        // Your task logic goes here
        return Result.success();
    }
}
```

5. In your Flutter code, call the platform-specific code to schedule the alarm:

```dart
import 'package:flutter/services.dart';

const platform = MethodChannel('your_channel');

Future<void> scheduleAlarm() async {
  try {
    await platform.invokeMethod('scheduleAlarm');
  } catch (e) {
    print('Error scheduling alarm: $e');
  }
}
```

6. In the Android-specific code, implement the `scheduleAlarm` method in the `MethodCallHandler`:

```java
import androidx.work.OneTimeWorkRequest;
import androidx.work.WorkManager;

public class MainActivity extends FlutterActivity implements MethodCallHandler {

    private static final String CHANNEL = "your_channel";

    ...

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        GeneratedPluginRegistrant.registerWith(this);

        // Set up the MethodChannel for communication with Flutter
        new MethodChannel(getFlutterView(), CHANNEL).setMethodCallHandler(this);
    }

    @Override
    public void onMethodCall(MethodCall call, Result result) {
        switch (call.method) {
            case "scheduleAlarm":
                scheduleAlarm();
                result.success(null);
                break;
            default:
                result.notImplemented();
                break;
        }
    }

    private void scheduleAlarm() {
        // Create an AlarmManager instance
        AlarmManager alarmManager = (AlarmManager) getSystemService(Context.ALARM_SERVICE);

        // Create a PendingIntent for the BroadcastReceiver
        Intent intent = new Intent(this, AlarmReceiver.class);
        PendingIntent alarmIntent = PendingIntent.getBroadcast(this, 0, intent, 0);

        // Set the alarm to trigger after a specific time or at regular intervals
        alarmManager.setInexactRepeating(AlarmManager.RTC_WAKEUP, System.currentTimeMillis(),
                AlarmManager.INTERVAL_DAY, alarmIntent);
    }
}
```

## Conclusion

By combining the Android `AlarmManager` with `WorkManager`, you can easily schedule tasks in a Flutter app that persist even when the app is not running or the device is rebooted. This allows you to build powerful features like notifications, periodic syncing, and more. Remember to use this powerful combination wisely and consider the impact on battery life and user experience. Happy scheduling!

**#Flutter #Android**