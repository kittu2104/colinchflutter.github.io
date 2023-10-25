---
layout: post
title: "How to schedule periodic tasks with background services in Flutter"
description: " "
date: 2023-10-25
tags: []
comments: true
share: true
---

In some cases, you may need to schedule periodic tasks to be executed in the background of your Flutter application. This could include tasks such as fetching data from an API, syncing data with a server, or sending notifications to the user. In Flutter, you can achieve this by using background services and scheduling tasks with the help of plugins.

## Prerequisites

Before we begin, make sure you have a basic understanding of Flutter and have set up your development environment.

## Choosing a Background Service Plugin

There are several plugins available for handling background services in Flutter. One of the commonly used plugins is the `workmanager` plugin. This plugin allows you to schedule tasks to be executed periodically even when your app is in the background or closed.

To add the `workmanager` plugin to your project, open your `pubspec.yaml` file and add the following dependency:

```yaml
dependencies:
  workmanager: ^0.4.0
```

Run `flutter pub get` to fetch the plugin.

## Configuring the Background Service

To configure the background service, you need to create a Dart file that extends the `Configuration` class provided by the `workmanager` plugin. This file will define the tasks to be executed and their schedules.

Create a new file named `background_service.dart` and add the following code:

```dart
import 'package:workmanager/workmanager.dart';

void callbackDispatcher() {
  Workmanager.executeTask((taskName, inputData) {
    // Your task logic goes here
    print("Background Task Executed");
    return Future.value(true);
  });
}

void main() {
  Workmanager.initialize(callbackDispatcher, isInDebugMode: true);
  Workmanager.registerPeriodicTask(
    "1",
    "backgroundTask",
    frequency: Duration(minutes: 15),
    initialDelay: Duration(minutes: 1),
  );
}
```

In the `callbackDispatcher` function, you can define the logic for your periodic task. In this example, we simply print a message when the task is executed.

The `main` function initializes the background service and registers a periodic task named "backgroundTask". The `frequency` parameter sets the interval between each execution of the task, while the `initialDelay` specifies the delay before the first execution.

## Running the Background Service

To run the background service, you need to configure your Flutter project to launch the background task when the app is closed or in the background.

Open your `AndroidManifest.xml` file located in the `android/app/src/main` directory and add the following lines inside the `<application>` tag:

```xml
<receiver android:name="com.example.workmanager.BackgroundBroadcastReceiver">
  <intent-filter>
    <action android:name="android.intent.action.BOOT_COMPLETED"/>
  </intent-filter>
</receiver>
```

Create a new file named `BackgroundBroadcastReceiver.java` inside the `android/app/src/main/java/com/example/workmanager` directory and add the following code:

```java
package com.example.workmanager;

import androidx.annotation.NonNull;

import io.flutter.embedding.android.FlutterActivity;
import io.flutter.embedding.engine.FlutterEngine;
import io.flutter.plugin.common.MethodChannel;
import io.flutter.plugins.GeneratedPluginRegistrant;
import io.flutter.view.FlutterMain;

public class BackgroundBroadcastReceiver extends FlutterActivity {
    @Override
    public void configureFlutterEngine(@NonNull FlutterEngine flutterEngine) {
        GeneratedPluginRegistrant.registerWith(flutterEngine);
        MethodChannel methodChannel = new MethodChannel(flutterEngine.getDartExecutor().getBinaryMessenger(), "com.example.workmanager");
        String args = getIntent().getStringExtra("args");
        BackgroundServiceImpl.initializeInBackground(this, args);
    }
}
```

This receiver is responsible for launching the background service and passing any necessary arguments to it.

## Scheduling the Background Task

To schedule the background task, you can invoke the `Workmanager().registerPeriodicTask` method from anywhere in your Flutter code. For example, you can schedule the task when the user performs a specific action or when the app is launched.

```dart
import 'package:workmanager/workmanager.dart';

void scheduleBackgroundTask() {
  Workmanager().registerPeriodicTask(
    "1",
    "backgroundTask",
    frequency: Duration(minutes: 15),
    initialDelay: Duration(minutes: 1),
  );
}
```

In this example, we schedule the task with the same parameters as specified in the `background_service.dart` file.

## Conclusion

Scheduling periodic tasks with background services in Flutter can be accomplished using the `workmanager` plugin. By properly configuring the background service and registering periodic tasks, you can ensure that your tasks are executed even when the app is closed or in the background.