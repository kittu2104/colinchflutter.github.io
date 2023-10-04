---
layout: post
title: "Working with notifications in scheduled tasks using WorkManager in Flutter"
description: " "
date: 2023-10-01
tags: [WorkManager]
comments: true
share: true
---

In mobile app development, it is common to schedule background tasks that need to be executed at specific times. One common use case is sending notifications to users at a predefined time. In Flutter, we can achieve this using the WorkManager package, which provides an easy way to schedule and execute background tasks.

## What is WorkManager?

WorkManager is a powerful library provided by the Android Jetpack that allows us to schedule and run background tasks on Android devices. It provides a consistent API to schedule tasks that need to run even if the app is closed or the device has restarted.

## Setting up WorkManager in Flutter

To use WorkManager in your Flutter project, you first need to add the `flutter_workmanager` package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_workmanager: ^0.3.0
```

After adding the package, make sure to run `flutter pub get` to fetch the dependencies.

## Creating a Background Task

To create a background task using WorkManager, we need to create a new class that extends the `Worker` class provided by the package. This class will contain the logic for our background task.

Here's an example of how to create a background task that sends a notification at a specific time:

```dart
import 'package:flutter_workmanager/flutter_workmanager.dart';

class NotificationWorker extends Worker {
  @override
  Future<void> performTask() async {
    // Add logic here to send notification

    // Example code for sending a notification using local_notifications package
    // import 'package:local_notifications/local_notifications.dart';
    // await LocalNotifications.createNotification(
    //   title: 'Notification',
    //   content: 'This is a notification',
    //   id: 0,
    // );

    return Future.value(true);
  }
}
```

In the `performTask()` method, you can implement the logic to send the notification. In this example, we have used the `local_notifications` package to send a notification, but you can use any other package that suits your requirements.

## Scheduling the Background Task

Once we have created the background task, we can schedule it to run at a specific time using WorkManager.

Here's an example of how to schedule the background task to run every day at a specific time:

```dart
import 'package:flutter_workmanager/flutter_workmanager.dart';

void scheduleNotificationTask() {
  FlutterWorkManager.initialize(callbackDispatcher);
  FlutterWorkManager.registerPeriodicTask(
    'notificationTask',
    'notificationTask',
    inputData: { },
    frequency: Duration(days: 1),
    existingWorkPolicy: ExistingWorkPolicy.replace,
  );
}

void callbackDispatcher() {
  FlutterWorkManager.executeTask((taskName, inputData) async {
    if (taskName == 'notificationTask') {
      // Create an instance of the background task and call performTask()
      NotificationWorker worker = NotificationWorker();
      await worker.performTask();
    }
  });
}
```

In the above example, `scheduleNotificationTask()` is called to initialize the WorkManager and register the periodic task. The `callbackDispatcher()` method is used to execute the background task when triggered by WorkManager.

## Conclusion

In this blog post, we have learned how to work with notifications in scheduled tasks using WorkManager in Flutter. WorkManager provides a convenient way to schedule and execute background tasks, allowing us to send notifications at specific times even if the app is closed or the device has restarted. By following the steps mentioned, you can easily implement scheduled notifications in your Flutter app. 

#flutter #WorkManager