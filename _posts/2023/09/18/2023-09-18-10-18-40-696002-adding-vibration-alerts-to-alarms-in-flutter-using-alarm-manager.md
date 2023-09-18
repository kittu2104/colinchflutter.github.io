---
layout: post
title: "Adding vibration alerts to alarms in Flutter using Alarm Manager"
description: " "
date: 2023-09-18
tags: [alarmmanager]
comments: true
share: true
---

In this blog post, we will discuss how to add vibration alerts to alarms in a Flutter application using the Alarm Manager package. The Alarm Manager package allows you to schedule and manage alarms in Flutter, making it convenient to implement features like alarms and reminders.

## Installing the Alarm Manager package

To get started, add the Alarm Manager package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_local_notifications: ^3.2.0
```

Then, run `flutter pub get` to fetch the package.

## Scheduling an alarm

To schedule an alarm, we will be using the `flutter_local_notifications` package along with the Alarm Manager package.

First, import the required dependencies:

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';
import 'package:android_alarm_manager/android_alarm_manager.dart';
```

Next, initialize the `FlutterLocalNotificationsPlugin` instance:

```dart
final FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin =
    FlutterLocalNotificationsPlugin();
```

Now, initialize the Alarm Manager and schedule an alarm with vibration:

```dart
void main() async {
  WidgetsFlutterBinding.ensureInitialized();

  final int vibrationPattern = AndroidAlarmManager.DEFAULT_VIBRATE_PATTERN;

  await AndroidAlarmManager.initialize();
  await flutterLocalNotificationsPlugin.initialize(
    InitializationSettings(
      android: AndroidInitializationSettings('@mipmap/ic_launcher'),
    ),
  );

  await AndroidAlarmManager.oneShot(
    const Duration(seconds: 5),
    0,
    showNotification,
    alarmClock: true,
    vibrationPattern: vibrationPattern,
  );

  runApp(MyApp());
}
```

In the above code, we set the `vibrationPattern` to `AndroidAlarmManager.DEFAULT_VIBRATE_PATTERN` to use the default vibration pattern. You can also define your own custom vibration patterns.

## Handling the alarm

To handle the alarm and show a notification, define the `showNotification` method:

```dart
void showNotification() async {
  const AndroidNotificationDetails androidPlatformChannelSpecifics =
      AndroidNotificationDetails('your_channel_id', 'your_channel_name',
          channelDescription: 'your_channel_description',
          importance: Importance.max,
          priority: Priority.high,
          vibrationPattern: AndroidAlarmManager.DEFAULT_VIBRATE_PATTERN);

  const NotificationDetails platformChannelSpecifics =
      NotificationDetails(android: androidPlatformChannelSpecifics);

  await flutterLocalNotificationsPlugin.show(
    0,
    'Alarm',
    'Time to wake up!',
    platformChannelSpecifics,
  );
}
```

In the above code, we define the `androidPlatformChannelSpecifics` with the necessary details for the notification, including the vibration pattern.

## Conclusion

In this blog post, we explored how to add vibration alerts to alarms in a Flutter application using the Alarm Manager package. By using the Flutter Local Notifications package in conjunction with the Alarm Manager package, we were able to easily schedule and manage alarms with vibration notifications.

#flutter #alarmmanager