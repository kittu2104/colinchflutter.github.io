---
layout: post
title: "Integrating Flutter Alarm Manager with local notifications"
description: " "
date: 2023-09-18
tags: [flutteralarmmanager]
comments: true
share: true
---

Flutter Alarm Manager is a handy package that allows you to schedule and manage alarms in your Flutter application. In combination with local notifications, it becomes a powerful tool for implementing alarm features.

## Setting Up Dependencies

To get started, you'll need to add the necessary dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_local_notifications: ^8.2.0
  flutter_alarm_manager: ^2.1.0
```

Make sure to run `flutter pub get` to fetch the packages.

## Initializing Flutter Local Notifications

First, let's set up Flutter Local Notifications. This package enables us to handle local notifications on Android and iOS platforms.

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';

FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin =
    FlutterLocalNotificationsPlugin();

void initializeNotifications() {
  var initializationSettingsAndroid =
      AndroidInitializationSettings('@drawable/ic_notification');
  var initializationSettingsIOS = IOSInitializationSettings();
  var initializationSettings = InitializationSettings(
      android: initializationSettingsAndroid, iOS: initializationSettingsIOS);

  flutterLocalNotificationsPlugin.initialize(initializationSettings);
}
```

In the code above, we create an instance of `FlutterLocalNotificationsPlugin` and initialize it with the appropriate settings for Android and iOS.

## Scheduling Alarms with Flutter Alarm Manager

Now, let's integrate Flutter Alarm Manager into our app.

```dart
import 'package:flutter_alarm_manager/flutter_alarm_manager.dart';

void scheduleAlarm(DateTime dateTime) async {
  await FlutterAlarmManager.cancelAll();

  // Schedule the alarm
  await FlutterAlarmManager.schedule(
    id: 0,
    // Alarm time
    dateTime: dateTime,
    // Callback function to be executed when the alarm triggers
    callback: _showNotification,
    // Optional interval for repeated alarms
    repeatInterval: const Duration(days: 1),
  );
}

void cancelAlarm() async {
  await FlutterAlarmManager.cancelAll();
}

void _showNotification() async {
  var androidPlatformChannelSpecifics = AndroidNotificationDetails(
      'channel_id', 'channel_name', 'channel_description',
      importance: Importance.max, priority: Priority.high);

  var iOSPlatformChannelSpecifics = IOSNotificationDetails();

  var platformChannelSpecifics = NotificationDetails(
      android: androidPlatformChannelSpecifics,
      iOS: iOSPlatformChannelSpecifics);

  await flutterLocalNotificationsPlugin.show(
    0,
    'Alarm',
    'Hello! It\'s time for your alarm.',
    platformChannelSpecifics,
  );
}
```

In the code above, we define the functions to schedule and cancel alarms using Flutter Alarm Manager. We also define the `_showNotification` function, which is the callback executed when the alarm triggers. This function shows a local notification using Flutter Local Notifications.

## Usage

To schedule an alarm, simply call the `scheduleAlarm` function with the desired alarm time:

```dart
scheduleAlarm(DateTime.now().add(Duration(minutes: 30)));
```

To cancel an alarm, call the `cancelAlarm` function:

```dart
cancelAlarm();
```

That's it! You now have a Flutter application that can schedule and manage alarms using Flutter Alarm Manager, and display local notifications using Flutter Local Notifications.

#flutter #flutteralarmmanager #flutterlocalnotifications