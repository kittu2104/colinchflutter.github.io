---
layout: post
title: "Working with push notifications in scheduled tasks using WorkManager in Flutter"
description: " "
date: 2023-10-01
tags: [workmanager, pushnotifications]
comments: true
share: true
---

In today's increasingly connected world, push notifications have become an integral part of our mobile applications. They allow us to send timely and relevant updates to our users even when our app is not running. In Flutter, we can leverage the WorkManager plugin to schedule push notifications as part of our scheduled tasks. In this blog post, we will learn how to integrate push notifications with scheduled tasks using WorkManager in Flutter.

## Prerequisites

Before we begin, make sure you have the following:

1. Flutter SDK installed on your machine.
2. A Flutter project set up using `flutter create`.
3. Basic knowledge of Flutter and Dart.

## Step 1: Add the WorkManager Plugin

To get started, we need to add the WorkManager plugin to our Flutter project. Open your project's `pubspec.yaml` file and add the following dependency:

```yaml
dependencies:
  workmanager: ^0.4.0
```

Save the file and run `flutter pub get` to fetch the dependencies.

## Step 2: Implementing the Scheduled Task

Now, let's dive into implementing the scheduled task that will trigger the push notification. We will create a new file called `notification_task.dart` and define a `NotificationTask` class that extends the `Task` class provided by WorkManager. This class will contain the logic for sending the push notification.

```dart
import 'package:workmanager/workmanager.dart';

class NotificationTask extends Task {
  @override
  Future<bool> callback() async {
    // Logic for sending the push notification
    // ...

    return true;
  }
}
```

In the `callback` method, you can write the necessary code to send the push notification. This can include fetching data from an API, generating the notification content, and invoking the platform-specific code to display the notification.

## Step 3: Scheduling the Task

Next, we need to schedule the task using WorkManager. Open the file where you want to schedule the task (e.g., `main.dart`), and add the following code:

```dart
import 'package:workmanager/workmanager.dart';
import 'notification_task.dart';

void main() {
  runApp(MyApp());
  scheduleNotificationTask();
}

void scheduleNotificationTask() {
  Workmanager.initialize(
    callbackDispatcher,
    isInDebugMode: true,
  );
  Workmanager.registerPeriodicTask(
    'notification_task',
    'notificationTask',
    frequency: Duration(hours: 24),
  );
}

void callbackDispatcher() {
  Workmanager.executeTask((task, inputData) {
    return NotificationTask().callback();
  });
}
```

The `scheduleNotificationTask` function initializes WorkManager and registers a periodic task called `'notification_task'` that will call the `NotificationTask` class every 24 hours. The `callbackDispatcher` function is responsible for executing the task.

## Step 4: Handle the Push Notification

Finally, we need to handle the push notification in our app. Add the necessary code to register for push notifications in your app initialization code. When a push notification is received, you can display it to the user by using a package like `flutter_local_notifications`.

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';

void main() {
  // ...

  registerForPushNotifications();

  runApp(MyApp());
}

void registerForPushNotifications() {
  // Code to register for push notifications
  // ...
}

void displayNotification(String title, String body) async {
  FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin =
      FlutterLocalNotificationsPlugin();
  var android = AndroidInitializationSettings('@mipmap/ic_launcher');
  var initializationSettings =
      InitializationSettings(android: android);
  flutterLocalNotificationsPlugin.initialize(initializationSettings);
  var notificationDetails =
      NotificationDetails(android: AndroidNotificationDetails('channel_id', 'channel_name', 'channel_description'));
  await flutterLocalNotificationsPlugin.show(
      0, title, body, notificationDetails);
}

```

The `displayNotification` function uses the `flutter_local_notifications` package to display a push notification with the provided `title` and `body`.

## Conclusion

Congratulations! You have successfully integrated push notifications with scheduled tasks using WorkManager in your Flutter application. This allows you to send timely and relevant updates to your users even when your app is not actively running. Feel free to explore more advanced features of WorkManager and customize the push notifications to suit your app's requirements.

#flutter #workmanager #pushnotifications