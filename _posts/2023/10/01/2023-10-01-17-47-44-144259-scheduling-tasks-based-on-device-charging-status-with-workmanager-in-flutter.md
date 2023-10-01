---
layout: post
title: "Scheduling tasks based on device charging status with WorkManager in Flutter"
description: " "
date: 2023-10-01
tags: [available(iOS, Flutter, WorkManager]
comments: true
share: true
---

In Flutter, you may often come across scenarios where you need to perform certain tasks when the device is charging. This could be helpful for scenarios like syncing data, performing backups, or updating the app when the device is connected to a power source.

To achieve this functionality, we can leverage the **WorkManager** plugin, which provides a way to schedule background work on Android and iOS devices. Here's how you can schedule tasks based on device charging status using WorkManager in your Flutter app.

## Step 1: Add the WorkManager plugin to your Flutter project

In your `pubspec.yaml` file, add the WorkManager plugin as a dependency:

```yaml
dependencies:
  flutter:
    sdk: flutter
  workmanager: ^latest_version
```

Run `flutter pub get` to fetch the dependencies.

## Step 2: Implement the charging status check and task scheduling

First, import the necessary packages in your Dart file:

```dart
import 'package:flutter/material.dart';
import 'package:workmanager/workmanager.dart';
import 'package:battery/battery.dart';
```

Next, implement the `startWorkManager` function:

```dart
void startWorkManager() {
  Workmanager.initialize(callbackDispatcher);
  Workmanager.registerPeriodicTask(
    'charge_task',
    'chargingTask',
    frequency: const Duration(minutes: 15),
    initialDelay: const Duration(seconds: 15),
  );
}

void callbackDispatcher() {
  Workmanager.executeTask((task, inputData) {
    if (task == 'chargingTask') {
      checkChargingStatus();
    }
    return Future.value(true);
  });
}

Future<void> checkChargingStatus() async {
  final battery = Battery();
  final status = await battery.batteryStatus;
  
  if (status == BatteryStatus.charging || status == BatteryStatus.full) {
    // Perform your desired task here
    // Your code logic goes here...
  }
}
```

The `startWorkManager` function initializes the WorkManager and registers a periodic task called "charge_task" that will execute the "chargingTask" callback every 15 minutes.

The `callbackDispatcher` function is the entry point for background tasks. It checks if the task is "chargingTask" and calls the `checkChargingStatus` function.

The `checkChargingStatus` function uses the `battery` package to check the device's battery status. If the status is either "charging" or "full", you can perform your desired task in the if block.

Remember to call `startWorkManager` in your app's initialization code, such as in the `main()` function.

## Step 3: Handling the background task in Android and iOS platforms

To handle background tasks in both Android and iOS, make the following platform-specific changes:

### Android:

1. Open the `AndroidManifest.xml` file located at `android/app/src/main/AndroidManifest.xml`.

2. Add the following `receiver` tag inside the `application` tag:

```xml
<receiver android:name="com.transistorsoft.flutter.backgroundfetch.BackgroundFetchBroadcastReceiver">
  <intent-filter>
    <action android:name="io.flutter.plugin.common.PluginRegistry.BackgroundFetch" />
  </intent-filter>
</receiver>
```

### iOS:

1. Open the `AppDelegate.swift` file located at `ios/Runner/AppDelegate.swift`.

2. Add the following code inside the `didFinishLaunchingWithOptions` method:

```swift
import Flutter
import FlutterPluginRegistrant
import workmanager

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    GeneratedPluginRegistrant.register(with: self)

    if #available(iOS 10.0, *) {
        WorkmanagerPlugin.setPluginRegistrantCallback { registry in
            FlutterWorkManagerPlugin.setPluginRegistrantCallback(registry)
        }
    }

    return super.application(application, didFinishLaunchingWithOptions: launchOptions)
}
```

That's it! You have now successfully scheduled tasks based on the device's charging status using WorkManager in your Flutter app.

Remember to handle any necessary permissions for background execution in your app to ensure a seamless experience for your users.

**#Flutter #WorkManager**