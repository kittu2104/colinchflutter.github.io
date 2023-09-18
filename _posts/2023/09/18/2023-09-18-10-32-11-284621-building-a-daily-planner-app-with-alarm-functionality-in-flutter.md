---
layout: post
title: "Building a daily planner app with alarm functionality in Flutter"
description: " "
date: 2023-09-18
tags: [dailyplanner]
comments: true
share: true
---

Are you looking to build a daily planner app with alarm functionality? Flutter is a powerful framework that allows you to create beautiful and feature-rich applications. In this tutorial, we will walk through the process of building a daily planner app with alarm functionality using Flutter.

## Setting Up the Flutter Project

First, make sure you have Flutter and Dart installed on your system. Once you have them installed, you can create a new Flutter project using the following command:

```bash
flutter create daily_planner
```

## Creating the User Interface

Next, we will create the user interface for our daily planner app. We will use the `flutter/material.dart` package to build our UI components. Start by opening the `lib/main.dart` file and replace its content with the following code:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(DailyPlannerApp());
}

class DailyPlannerApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Daily Planner',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: HomePage(),
    );
  }
}

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Daily Planner'),
      ),
      body: Container(
        child: Center(
          child: Text('Welcome to the Daily Planner App!'),
        ),
      ),
    );
  }
}
```

The code above sets up the basic structure of our app and displays a simple welcome message on the home page.

## Adding Alarm Functionality

To add alarm functionality to our daily planner app, we will use the `flutter_local_notifications` package. This package provides an easy way to schedule, display, and handle notifications in Flutter. To install the package, add it to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter

  flutter_local_notifications: ^x.x.x # Replace with the latest version
```

Replace `x.x.x` with the latest version of the package.

Next, create a new file `lib/alarm_service.dart` and add the following code:

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';

class AlarmService {
  Future<void> scheduleAlarm(DateTime scheduledTime, String message) async {
    FlutterLocalNotificationsPlugin notificationsPlugin =
        FlutterLocalNotificationsPlugin();

    const AndroidInitializationSettings initializationSettingsAndroid =
        AndroidInitializationSettings('app_icon');

    final InitializationSettings initializationSettings =
        InitializationSettings(
      android: initializationSettingsAndroid,
    );

    await notificationsPlugin.initialize(initializationSettings);

    const AndroidNotificationDetails androidPlatformChannelSpecifics =
        AndroidNotificationDetails(
      'daily_planner_channel',
      'Daily Planner',
      'Channel for Daily Planner Alarm',
      importance: Importance.max,
      priority: Priority.high,
    );

    const NotificationDetails platformChannelSpecifics = NotificationDetails(
      android: androidPlatformChannelSpecifics,
    );

    await notificationsPlugin.schedule(
      0,
      'Daily Planner Alarm',
      message,
      scheduledTime,
      platformChannelSpecifics,
    );
  }
}
```

In the code above, we create an `AlarmService` class with a `scheduleAlarm` method that takes a `scheduledTime` and `message` as arguments. This method initializes the `FlutterLocalNotificationsPlugin`, sets up the notification channel, and schedules the alarm.

To use the `AlarmService` in our app, open the `lib/main.dart` file and replace the `HomePage` widget with the following code:

```dart
class HomePage extends StatelessWidget {
  final AlarmService alarmService = AlarmService();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Daily Planner'),
      ),
      body: Container(
        child: Center(
          child: RaisedButton(
            child: Text('Schedule Alarm'),
            onPressed: () {
              // Set the scheduled time and message
              DateTime scheduledTime = DateTime.now().add(Duration(minutes: 1));
              String message = 'Time to plan your day!';

              // Schedule the alarm
              alarmService.scheduleAlarm(scheduledTime, message);
            },
          ),
        ),
      ),
    );
  }
}
```

The code above creates an instance of the `AlarmService` and schedules an alarm when the user taps on the "Schedule Alarm" button.

## Conclusion

In this tutorial, we have learned how to build a daily planner app with alarm functionality using Flutter. We have covered setting up the project, creating the user interface, and adding alarm functionality using the `flutter_local_notifications` package. With this knowledge, you can expand the app by allowing users to add tasks and reminders to their daily planner. Enjoy building your daily planner app! #flutter #dailyplanner