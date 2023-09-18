---
layout: post
title: "Customizing alarm notifications in Flutter with Alarm Manager"
description: " "
date: 2023-09-18
tags: [alarmmanager]
comments: true
share: true
---
In a mobile application, it is often necessary to schedule and customize alarm notifications. Flutter provides a powerful package called `flutter_local_notifications` that allows you to schedule and handle alarm notifications easily. In this article, we will explore how to customize alarm notifications using Flutter's Alarm Manager and the `flutter_local_notifications` package.

## Prerequisites
Before we begin, make sure you have the latest version of Flutter and the `flutter_local_notifications` package installed in your Flutter project. You can add the package to your `pubspec.yaml` file as follows:

```dart
dependencies:
  flutter_local_notifications: ^6.0.0
```

## Basic Setup
To get started, import the necessary classes from the `flutter_local_notifications` package:

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';
```

Next, initialize the `FlutterLocalNotificationsPlugin` and register the initialization settings. This step is usually performed in the `main` method of your Flutter application:

```dart
void main() async {
  WidgetsFlutterBinding.ensureInitialized();

  final FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin =
      FlutterLocalNotificationsPlugin();

  const AndroidInitializationSettings initializationSettingsAndroid =
      AndroidInitializationSettings('app_icon');

  final InitializationSettings initializationSettings =
      InitializationSettings(android: initializationSettingsAndroid);

  await flutterLocalNotificationsPlugin.initialize(initializationSettings);
  runApp(MyApp());
}
```

Here, we are initializing the `FlutterLocalNotificationsPlugin` and providing the path to the app icon as `app_icon`. You can replace `"app_icon"` with your actual app icon file name.

## Scheduling Alarm Notifications
Now, let's see how to schedule alarm notifications using the `flutter_local_notifications` package. To schedule a notification, you need to provide a unique identifier for the notification, the title, body, and the time at which it should be triggered.

```dart
void scheduleAlarmNotification(DateTime scheduledTime) async {
  const AndroidNotificationDetails androidPlatformChannelSpecifics =
      AndroidNotificationDetails(
    'channel_id',
    'channel_name',
    'channel_description',
    importance: Importance.max,
    priority: Priority.high,
    enableLights: true,
    enableVibration: true,
  );

  const NotificationDetails platformChannelSpecifics =
      NotificationDetails(android: androidPlatformChannelSpecifics);

  await flutterLocalNotificationsPlugin.zonedSchedule(
    0,
    'Alarm Title',
    'Alarm Body',
    scheduledTime,
    platformChannelSpecifics,
    uiLocalNotificationDateInterpretation: UILocalNotificationDateInterpretation.absoluteTime,
    androidAllowWhileIdle: true,
  );
}
```

In the above code snippet, we are using the `zonedSchedule` method to schedule the alarm notification. We provide a unique identifier (here, `0`), the title and body of the notification, the scheduled time, and the notification details (`platformChannelSpecifics`).

## Customizing Alarm Notifications
Now, let's see how we can customize the alarm notifications. Suppose you want to change the color of the notification LED and add a custom sound. You can modify the `androidPlatformChannelSpecifics` as follows:

```dart
const AndroidNotificationDetails androidPlatformChannelSpecifics =
      AndroidNotificationDetails(
    'channel_id',
    'channel_name',
    'channel_description',
    importance: Importance.max,
    priority: Priority.high,
    enableLights: true,
    lightColor: Colors.red,
    enableVibration: true,
    sound: RawResourceAndroidNotificationSound('custom_notification_sound'),
    playSound: true,
  );
```

In the above code snippet, we have added the `lightColor` property to set the LED color to red. We have also set the custom sound using the `RawResourceAndroidNotificationSound` class and the `sound` property.

## Conclusion
In this tutorial, we learned how to customize alarm notifications in Flutter using the Alarm Manager and the `flutter_local_notifications` package. We explored how to schedule alarm notifications and customize them with different settings. Now you can implement personalized alarm notifications in your Flutter applications.

#flutter #alarmmanager