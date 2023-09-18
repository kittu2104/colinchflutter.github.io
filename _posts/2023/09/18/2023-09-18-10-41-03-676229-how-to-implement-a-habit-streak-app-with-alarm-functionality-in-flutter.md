---
layout: post
title: "How to implement a habit streak app with alarm functionality in Flutter"
description: " "
date: 2023-09-18
tags: [HabitStreakApp]
comments: true
share: true
---

In today's fast-paced world, it can be challenging to stay consistent with our habits. To help with this, implementing a habit streak app with alarm functionality can be a great way to track and remind ourselves of our daily habits. In this tutorial, we will explore how to build a habit streak app with alarm functionality using Flutter.

## Prerequisites

Before we begin, make sure you have the following prerequisites installed:

- Flutter SDK
- Android Studio or any other preferred code editor

## Step 1: Setting Up the Flutter Project

1. Open Android Studio and click on "Create New Flutter Project".
2. Select a project location and give it a name.
3. Choose your desired Flutter SDK path and click "Next".
4. Choose your preferred language and click "Finish".

## Step 2: Designing the App UI

Now, let's design the user interface of our habit streak app. We will start by creating a new Dart file named `home_screen.dart` and adding the necessary code to define the UI of our home screen.

```dart
import 'package:flutter/material.dart';

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Habit Streak App'),
      ),
      body: Center(
        child: Text(
          'Welcome to the Habit Streak App!',
          style: TextStyle(
            fontSize: 24,
            fontWeight: FontWeight.bold,
          ),
        ),
      ),
    );
  }
}
```

## Step 3: Implementing Alarm Functionality

To implement alarm functionality, we will use the `flutter_local_notifications` package. Add the package dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_local_notifications: ^2.0.0+1
```

Now, let's create a new Dart file named `alarm_service.dart` and add the following code to set up and schedule notifications:

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';

class AlarmService {
  final FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin =
      FlutterLocalNotificationsPlugin();

  Future<void> init() async {
    final AndroidInitializationSettings initializationSettingsAndroid =
        AndroidInitializationSettings('@mipmap/ic_launcher');
    final InitializationSettings initializationSettings =
        InitializationSettings(android: initializationSettingsAndroid);

    await flutterLocalNotificationsPlugin.initialize(initializationSettings);
  }

  Future<void> scheduleNotification() async {
    final AndroidNotificationDetails androidPlatformChannelSpecifics =
        AndroidNotificationDetails(
      'habit_streak_channel',
      'Habit Streak Channel',
      'Channel for Habit Streak App Notifications',
      importance: Importance.high,
      priority: Priority.high,
    );
    final NotificationDetails platformChannelSpecifics =
        NotificationDetails(android: androidPlatformChannelSpecifics);

    await flutterLocalNotificationsPlugin.zonedSchedule(
      0,
      'Habit Reminder',
      'Remember to complete your habit today!',
      _nextInstanceOfTenAM(),
      platformChannelSpecifics,
      androidAllowWhileIdle: true,
      uiLocalNotificationDateInterpretation:
          UILocalNotificationDateInterpretation.absoluteTime,
    );
  }

  tz.TZDateTime _nextInstanceOfTenAM() {
    final tz.TZDateTime now = tz.TZDateTime.now(tz.local);
    tz.TZDateTime scheduledDate =
        tz.TZDateTime(tz.local, now.year, now.month, now.day, 10);
    if (scheduledDate.isBefore(now)) {
      scheduledDate = scheduledDate.add(Duration(days: 1));
    }
    return scheduledDate;
  }
}
```

## Step 4: Using the Alarm Service and Completing the UI

Now, let's update the `home_screen.dart` file to integrate the alarm functionality and complete the UI.

```dart
import 'package:flutter/material.dart';

import 'alarm_service.dart';

class HomeScreen extends StatefulWidget {
  @override
  _HomeScreenState createState() => _HomeScreenState();
}

class _HomeScreenState extends State<HomeScreen> {
  final AlarmService _alarmService = AlarmService();

  @override
  void initState() {
    super.initState();
    _initializeAlarmService();
  }

  Future<void> _initializeAlarmService() async {
    await _alarmService.init();
    await _alarmService.scheduleNotification();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Habit Streak App'),
      ),
      body: Center(
        child: Text(
          'Welcome to the Habit Streak App!',
          style: TextStyle(
            fontSize: 24,
            fontWeight: FontWeight.bold,
          ),
        ),
      ),
    );
  }
}
```

## Step 5: Running the App

Once you've completed all the steps, run your app using the `flutter run` command and see the magic happen! You should see the "Habit Streak App" title in the app bar and the "Welcome to the Habit Streak App!" text in the center of the screen. The alarm service will also schedule a notification for 10 AM.

Congratulations! You have successfully implemented a habit streak app with alarm functionality in Flutter. Feel free to customize the UI and add more features to make the app more interactive and user-friendly.

#Flutter #HabitStreakApp