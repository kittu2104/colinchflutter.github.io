---
layout: post
title: "Using Flutter Alarm Manager to schedule tasks or reminders"
description: " "
date: 2023-09-18
tags: [AlarmManager]
comments: true
share: true
---

In this blog post, we will explore how to utilize the Flutter Alarm Manager package to schedule tasks or reminders in your Flutter application. 

## What is Flutter Alarm Manager?

Flutter Alarm Manager is a Flutter plugin that provides a way to schedule platform-specific alarms. It allows you to schedule one-time or recurring tasks or reminders to be executed at specified times.

### Installation

To get started, add the `flutter_alarm_manager` package dependency to your project's `pubspec.yaml` file:

```yaml
dependencies:
  flutter_alarm_manager: ^2.0.0
```

## Scheduling a Task or Reminder

To schedule a task or reminder, follow these steps:

1. Import the necessary packages:

```dart
import 'package:flutter_alarm_manager/flutter_alarm_manager.dart';
import 'package:flutter_local_notifications/flutter_local_notifications.dart';
```

2. Initialize the `FlutterAlarmManager` and `FlutterLocalNotificationsPlugin` instances:

```dart
final FlutterAlarmManager _alarmManager = FlutterAlarmManager();
final FlutterLocalNotificationsPlugin _notificationsPlugin =
      FlutterLocalNotificationsPlugin();
```

3. Configure the notification settings using the `AndroidInitializationSettings` and `IOSInitializationSettings` classes:

```dart
final initializationSettingsAndroid = AndroidInitializationSettings('app_icon');
final initializationSettingsIOS = IOSInitializationSettings();
final initializationSettings = InitializationSettings(
      android: initializationSettingsAndroid,
      iOS: initializationSettingsIOS,
);
await _notificationsPlugin.initialize(initializationSettings);
```

4. Create a function to display the notification:

```dart
Future<void> _displayNotification(
      String title, String body, int id, DateTime scheduledDateTime) async {
    const androidPlatformChannelSpecifics = AndroidNotificationDetails(
      'your_channel_id',
      'your_channel_name',
      'your_channel_description',
      importance: Importance.max,
      priority: Priority.high,
      ticker: 'ticker',
    );
    const iOSPlatformChannelSpecifics =
        IOSNotificationDetails();
    const platformChannelSpecifics = NotificationDetails(
        android: androidPlatformChannelSpecifics,
        iOS: iOSPlatformChannelSpecifics);
    await _notificationsPlugin.zonedSchedule(
      id,
      title,
      body,
      tz.TZDateTime.from(scheduledDateTime, tz.local),
      platformChannelSpecifics,
      androidAllowWhileIdle: true,
      uiLocalNotificationDateInterpretation:
          UILocalNotificationDateInterpretation.absoluteTime,
    );
  }
```

5. Schedule the task or reminder using the `_alarmManager` instance:

```dart
_alarmManager.schedule(
      id,
      scheduledDateTime.millisecondsSinceEpoch,
      _callback,
      alarmType: AlarmType.RTC_WAKEUP,
      alarmAction: AlarmAction.ACTION_ALARM_RECEIVER,
      allowWhileIdle: true,
)
```

### Example Usage

Here's an example of how to schedule a task or reminder:

```dart
void _scheduleTask(DateTime scheduledDateTime) {
    final notificationId = DateTime.now().millisecondsSinceEpoch;
    _displayNotification(
      'Task Reminder',
      'You have an upcoming task to complete.',
      notificationId,
      scheduledDateTime,
    );
    _alarmManager.schedule(
      notificationId,
      scheduledDateTime.millisecondsSinceEpoch,
      _callback,
      alarmType: AlarmType.RTC_WAKEUP,
      alarmAction: AlarmAction.ACTION_ALARM_RECEIVER,
      allowWhileIdle: true,
    );
}
```

## Conclusion

In this blog post, we learned how to use the Flutter Alarm Manager plugin to schedule tasks or reminders in a Flutter application. You can leverage this package to enhance the productivity and user experience of your application by providing timely notifications and reminders to your users.

By using Flutter Alarm Manager, you can streamline and automate task scheduling and reminders, making your app even more efficient. So go ahead and implement this powerful plugin in your Flutter project and enhance your application's functionality.

#Flutter #AlarmManager