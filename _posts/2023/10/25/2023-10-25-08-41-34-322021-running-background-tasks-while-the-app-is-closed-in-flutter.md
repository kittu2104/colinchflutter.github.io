---
layout: post
title: "Running background tasks while the app is closed in Flutter"
description: " "
date: 2023-10-25
tags: []
comments: true
share: true
---

When developing mobile applications, there may be instances where you need to run certain tasks even when the app is closed. This could include fetching new data, syncing data with a server, or performing other background tasks. In this article, we will explore how to achieve background task execution in Flutter.

## 1. Using the background_fetch Plugin

Flutter provides a handy plugin called `background_fetch` that allows you to register periodic background tasks on both iOS and Android platforms. This plugin utilizes the platform-specific APIs and works even when your app is closed.

To use the `background_fetch` plugin, follow these steps:

### Step 1: Add the Dependency

Add the `background_fetch` package as a dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  background_fetch: ^0.9.3
```

### Step 2: Configure the Background Task

In your Flutter application, configure the background task with desired settings. This usually involves specifying the interval at which the task should run:

```dart
import 'package:background_fetch/background_fetch.dart';

void main() {
  BackgroundFetch.registerHeadlessTask(myBackgroundTask);
  runApp(MyApp());
}

void myBackgroundTask(String taskId) async {
  // Perform your background task here
  // This method will be called periodically based on your configuration
  // Remember to handle any asynchronous operations accordingly
  BackgroundFetch.finish(taskId);
}
```

In the above code, we register a headless task `myBackgroundTask` using `BackgroundFetch.registerHeadlessTask`. This task will be executed periodically in the background when your app is closed.

### Step 3: Configure Platform-Specific Settings

For both iOS and Android, you need to perform additional configuration steps specific to each platform.

#### iOS Configuration

In your `AppDelegate.m` file (for Objective-C) or `AppDelegate.swift` file (for Swift), add the following code:

```swift
import UIKit
import Flutter
import background_fetch

@UIApplicationMain
@objc class AppDelegate: FlutterAppDelegate {
  override func application(
    _ application: UIApplication,
    didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?
  ) -> Bool {
    GeneratedPluginRegistrant.register(with: self)
    BackgroundFetch.registerHeadlessTask(scheduler.TaskRunner().shouldExecuteTask)
    return super.application(application, didFinishLaunchingWithOptions: launchOptions)
  }
}
```

Note that `registerHeadlessTask` is called inside the `didFinishLaunchingWithOptions` method.

#### Android Configuration

In your `MainActivity.kt` file, add the following code:

```kotlin
import io.flutter.embedding.android.FlutterActivity
import io.flutter.embedding.engine.FlutterEngine
import com.transistorsoft.flutter.backgroundfetch.BackgroundFetchPlugin

class MainActivity: FlutterActivity() {
  override fun configureFlutterEngine(flutterEngine: FlutterEngine) {
    super.configureFlutterEngine(flutterEngine)
    BackgroundFetchPlugin.registerWith(flutterEngine.dartExecutor.binaryMessenger)
  }
}
```

This code snippet registers the `BackgroundFetchPlugin` with the `FlutterEngine`.

## 2. Scheduling Periodic Background Tasks

Now that you have set up the `background_fetch` plugin, you can schedule periodic background tasks based on your app's requirements:

```dart
void configureBackgroundTasks() {
  BackgroundFetch.configure(
    BackgroundFetchConfig(
       minimumFetchInterval: 15,
       stopOnTerminate: false,
       enableHeadless: true,
       requiresBatteryNotLow: false,
       requiresCharging: false,
       requiresStorageNotLow: false,
       disableAutoStart: false,
       requiredNetworkType: NetworkType.NONE,
     ),
     myBackgroundTask,
  );
}
```

In the above example, we configure the background task with a minimum fetch interval of 15 minutes and other optional settings. The `myBackgroundTask` method will be invoked periodically based on this configuration.

## Conclusion

By using the `background_fetch` plugin in Flutter, you can easily run background tasks even when your app is closed. This allows you to keep your app up to date and perform necessary operations in the background. Remember to follow the platform-specific configuration steps for iOS and Android.