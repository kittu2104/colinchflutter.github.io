---
layout: post
title: "Scheduling tasks at specific times using WorkManager in Flutter"
description: " "
date: 2023-10-01
tags: [workmanager]
comments: true
share: true
---

## Introduction
In Flutter, you may need to schedule tasks to run at specific times, such as sending notifications, updating data, or performing background processing. One way to accomplish this is by utilizing WorkManager, a powerful plugin that allows you to schedule recurring and one-time tasks in your Flutter app. In this tutorial, we will walk through the steps to schedule tasks at specific times using WorkManager.

## Prerequisites
Before proceeding, make sure you have the following:

- Flutter SDK installed
- Android Studio with Flutter and Dart plugins
- A basic understanding of Flutter programming

## Step 1: Installing the WorkManager plugin
To get started, open your Flutter project in Android Studio or your preferred IDE. Then, add the WorkManager plugin to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  workmanager: ^0.4.1-nullsafety.1
```

Save the file, and then run `flutter pub get` to install the plugin.

## Step 2: Configuring the WorkManager
In this step, we will configure the WorkManager to run tasks at specific times. Create a new Dart file, such as `workmanager_config.dart`, and add the following code:

```dart
import 'package:workmanager/workmanager.dart';

void callbackDispatcher() {
  Workmanager.executeTask((task, inputData) {
    // Implement your task logic here
    // This method will be called when the scheduled task is triggered
    return Future.value(true);
  });
}

void main() {
  Workmanager.initialize(callbackDispatcher);
  Workmanager.registerPeriodicTask(
    "myTaskName",
    "myTaskTag",
    initialDelay: Duration(minutes: 15), // Delay before the first execution
    frequency: Duration(hours: 24), // Repeat every 24 hours
  );
}
```

In the above code, we define a `callbackDispatcher` function that will be called when the scheduled task is triggered. Inside this function, you can implement your own task logic.

The `main` function initializes and configures the WorkManager. We register a periodic task with a unique name and tag using the `registerPeriodicTask` method. You can adjust the initial delay and frequency as per your requirements.

## Step 3: Requesting necessary permissions
To run background tasks on Android, we need to request the necessary permissions. Open the `AndroidManifest.xml` file located in the `android/app/src/main` directory of your Flutter project, and add the following permissions:

```xml
<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
<uses-permission android:name="android.permission.REQUEST_IGNORE_BATTERY_OPTIMIZATIONS" />
<uses-permission android:name="android.permission.WAKE_LOCK" />
```

## Step 4: Run the scheduled task
To run the scheduled task, call the `runBackgroundTask` method wherever you want to schedule the task. For example, you can call it inside a button's `onPressed` callback:

```dart
import 'package:workmanager/workmanager.dart';

void runBackgroundTask() async {
  await Workmanager.initialize(callbackDispatcher);
  await Workmanager.registerPeriodicTask(
    "myTaskName",
    "myTaskTag",
    initialDelay: Duration(minutes: 15),
    frequency: Duration(hours: 24),
  );
}

// Inside a button's onPressed callback
runBackgroundTask();
```

## Conclusion
In this tutorial, we learned how to schedule tasks at specific times using WorkManager in Flutter. By configuring the WorkManager and registering periodic tasks, you can ensure your app performs background processing or runs specific actions automatically. WorkManager offers flexibility and reliability, making it an excellent choice for scheduling tasks in Flutter applications.

#flutter #workmanager