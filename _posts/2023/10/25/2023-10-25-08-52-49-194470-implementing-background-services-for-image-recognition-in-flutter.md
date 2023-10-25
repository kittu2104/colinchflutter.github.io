---
layout: post
title: "Implementing background services for image recognition in Flutter"
description: " "
date: 2023-10-25
tags: [BackgroundServices]
comments: true
share: true
---

In this blog post, we will explore how to implement background services for image recognition in Flutter, allowing your app to seamlessly process images even when it is not in the foreground.

## Table of Contents
- [Introduction](#introduction)
- [Using Flutter Workmanager](#using-flutter-workmanager)
- [Using Android AlarmManager and Flutter MethodChannel](#using-android-alarmmanager-and-flutter-methodchannel)
- [Conclusion](#conclusion)

## Introduction

Background services are essential for performing resource-intensive tasks, such as image recognition, without disturbing the user experience. Flutter provides different approaches to implement background services in your application. In this post, we will focus on two popular methods: using Flutter Workmanager and using Android AlarmManager and Flutter MethodChannel.

## Using Flutter Workmanager

Flutter Workmanager is a plugin that helps you run tasks periodically or in the background using simple configuration. To implement image recognition in the background using Flutter Workmanager, follow these steps:

1. Add the Flutter Workmanager plugin to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_workmanager: ^0.2.3
```

2. Create a Dart file to handle the background work, for example, `image_recognition_worker.dart`. This file should extend the `Worker` class from the Flutter Workmanager plugin and override the `doWork` method. Inside the `doWork` method, you can perform your image recognition tasks.

```dart
import 'package:flutter_workmanager/flutter_workmanager.dart';

class ImageRecognitionWorker extends Worker {
  @override
  Future<void> doWork() async {
    // Perform image recognition tasks here
    // ...
  }
}
```

3. Register the worker in the `main.dart` file:

```dart
import 'package:flutter_workmanager/flutter_workmanager.dart';

void callbackDispatcher() {
  Workmanager.executeTask((task, inputData) {
    // Handle incoming task here
    // ...
    return Future.value(true);
  });
}

void main() {
  // Initialize Workmanager
  WidgetsFlutterBinding.ensureInitialized();
  Workmanager.initialize(callbackDispatcher, isInDebugMode: false);
  Workmanager.registerOneOffTask(
    "imageRecognitionTask",
    "image_recognition_task",
    initialDelay: Duration(seconds: 5),
  );
}
```

4. Finally, start the background service by calling `Workmanager.registerOneOffTask` in the `main` function. This will execute the image recognition task after a specified initial delay.

Using this approach, you can seamlessly run image recognition tasks in the background, even when the app is not in the foreground.

## Using Android AlarmManager and Flutter MethodChannel

Another approach to implement background services for image recognition in Flutter is by utilizing the Android AlarmManager and Flutter MethodChannel.

1. Create a Dart class to handle the image recognition tasks, for example, `ImageRecognitionHandler.dart`. This class should wrap the image recognition functionality using platform-specific code via Flutter MethodChannel.

```dart
import 'package:flutter/services.dart';

class ImageRecognitionHandler {
  static const MethodChannel _channel =
      MethodChannel('image_recognition_channel');

  static Future<void> recognizeImage() async {
    try {
      await _channel.invokeMethod('recognizeImage');
    } catch (e) {
      print('Error invoking method: $e');
    }
  }
}
```

2. In the Android project, create a `MainActivity.kt` file:

```kotlin
import io.flutter.embedding.android.FlutterActivity
import io.flutter.embedding.engine.FlutterEngine
import io.flutter.plugins.GeneratedPluginRegistrant
import android.app.AlarmManager
import android.app.PendingIntent
import android.content.Context
import android.content.Intent
import android.os.Build
import androidx.annotation.NonNull

class MainActivity: FlutterActivity() {
    private val CHANNEL = "image_recognition_channel"

    override fun configureFlutterEngine(@NonNull flutterEngine: FlutterEngine) {
        GeneratedPluginRegistrant.registerWith(flutterEngine)

        // Create MethodChannel
        MethodChannel(flutterEngine.dartExecutor.binaryMessenger, CHANNEL)
            .setMethodCallHandler { call, result ->
                if (call.method == "recognizeImage") {
                    // Perform image recognition tasks here
                    // ...
                    result.success(true)
                } else {
                    result.notImplemented()
                }
            }
    }

    override fun onResume() {
        super.onResume()
        
        // Check if the app was started from the background due to alarm
        val startedFromAlarm = intent?.getBooleanExtra("startedFromAlarm", false) ?: false
        if (startedFromAlarm) {
            // Perform image recognition tasks here
            // ...
        }
    }

    override fun onDestroy() {
        super.onDestroy()
        scheduleBackgroundService()
    }

    private fun scheduleBackgroundService() {
        val alarmManager = getSystemService(Context.ALARM_SERVICE) as AlarmManager
        val intent = Intent(this, MainActivity::class.java)
        intent.putExtra("startedFromAlarm", true)
        val pendingIntent = if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
            PendingIntent.getActivity(
                this, 0, intent, PendingIntent.FLAG_UPDATE_CURRENT or PendingIntent.FLAG_IMMUTABLE
            )
        } else {
            PendingIntent.getActivity(this, 0, intent, PendingIntent.FLAG_UPDATE_CURRENT)
        }
        val triggerTime = System.currentTimeMillis() + (5 * 60 * 1000) // Run every 5 minutes
        alarmManager.setExactAndAllowWhileIdle(
            AlarmManager.RTC_WAKEUP, triggerTime, pendingIntent
        )
    }
}
```

3. In the `AndroidManifest.xml` file, add the following permissions:

```xml
<uses-permission android:name="android.permission.REQUEST_IGNORE_BATTERY_OPTIMIZATIONS"/>
<uses-permission android:name="android.permission.WAKE_LOCK"/>
```

4. Run the code and the image recognition tasks will now run periodically. The background service will be started by the AlarmManager, and the app will perform image recognition every 5 minutes in the background.

## Conclusion

In this blog post, we explored two methods for implementing background services for image recognition in Flutter. By utilizing Flutter Workmanager or combining Android AlarmManager with Flutter MethodChannel, you can seamlessly perform image recognition tasks even when your app is not in the foreground. Incorporate these techniques in your Flutter app to enhance functionality and user experience.

**References:**
- [Flutter Workmanager](https://pub.dev/packages/flutter_workmanager)
- [Android AlarmManager](https://developer.android.com/reference/android/app/AlarmManager)
- [Flutter MethodChannel](https://api.flutter.dev/flutter/services/MethodChannel-class.html)

Tags: #Flutter #BackgroundServices