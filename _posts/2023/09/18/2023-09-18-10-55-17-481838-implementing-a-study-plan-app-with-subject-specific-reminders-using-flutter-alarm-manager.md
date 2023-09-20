---
layout: post
title: "Implementing a study plan app with subject-specific reminders using Flutter Alarm Manager"
description: " "
date: 2023-09-18
tags: [studyplan]
comments: true
share: true
---

In today's fast-paced world, staying organized and managing time effectively is crucial, especially for students. With the help of technology, we can simplify the process of creating and following a study plan. In this tutorial, we will learn how to implement a study plan app using Flutter Alarm Manager, which will send subject-specific reminders to keep us on track. Let's get started!

## Prerequisites

Before we begin, make sure you have the following prerequisites in place:

1. Flutter SDK: Install Flutter on your machine by following the official documentation.
2. Flutter Alarm Manager Package: Add the `flutter_alarm_manager` package to your Flutter project by adding it as a dependency in your `pubspec.yaml` file.

## Setting up the App

1. Create a new Flutter project by running the following command in your terminal:

```bash
flutter create study_plan_app
```

2. Open the project in your favorite code editor.

3. Remove the default code in the `lib/main.dart` file and replace it with the following code:

```dart
import 'package:flutter/material.dart';

void main() => runApp(StudyPlanApp());

class StudyPlanApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Study Plan',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: StudyPlanScreen(),
    );
  }
}

class StudyPlanScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Study Plan'),
      ),
      body: Container(
        child: Center(
          child: Text(
            'Welcome to the Study Plan App!',
            style: TextStyle(fontSize: 20),
          ),
        ),
      ),
    );
  }
}
```

This code sets up a basic Flutter app with a home screen that displays a welcome message.

## Adding Subject-Specific Reminders

Now, let's add the functionality to set subject-specific reminders using Flutter Alarm Manager.

1. Add the `flutter_local_notifications` package to your project by adding it as a dependency in your `pubspec.yaml` file.

2. Import the necessary packages in your `lib/main.dart` file:

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';
import 'package:flutter_alarm_manager/flutter_alarm_manager.dart';
```

3. Update the `StudyPlanScreen` class to include a button to set a reminder. Replace the existing code in the `StudyPlanScreen` class with the following code:

```dart
class StudyPlanScreen extends StatefulWidget {
  @override
  _StudyPlanScreenState createState() => _StudyPlanScreenState();
}

class _StudyPlanScreenState extends State<StudyPlanScreen> {
  FlutterLocalNotificationsPlugin? flutterLocalNotificationsPlugin;

  @override
  void initState() {
    super.initState();
    flutterLocalNotificationsPlugin = FlutterLocalNotificationsPlugin();
    const AndroidInitializationSettings initializationSettingsAndroid =
        AndroidInitializationSettings('@mipmap/ic_launcher');
    final InitializationSettings initializationSettings =
        InitializationSettings(
      android: initializationSettingsAndroid,
      iOS: null,
    );
    flutterLocalNotificationsPlugin!.initialize(initializationSettings);
  }

  Future<void> _scheduleNotification() async {
    const int notificationId = 0;
    const String notificationTitle = 'Study Reminder';
    const String notificationBody = 'Time to study ${selectedSubject}';

    final DateTime now = DateTime.now();
    final DateTime scheduledNotificationDateTime =
        DateTime(now.year, now.month, now.day, selectedHour, selectedMinute);

    await FlutterAlarmManager.periodic(
      const Duration(minutes: 1),
      notificationId,
      _showNotification,
    );
  }

  Future<void> _showNotification() async {
    const int channelId = 0;
    const String channelName = 'Study Reminder Channel';
    const String channelDescription = 'Reminders for study sessions';

    final AndroidNotificationDetails androidPlatformChannelSpecifics =
        AndroidNotificationDetails(
      '${channelId}',
      channelName,
      channelDescription,
      importance: Importance.high,
      priority: Priority.high,
    );

    const NotificationDetails platformChannelSpecifics =
        NotificationDetails(android: androidPlatformChannelSpecifics);

    await flutterLocalNotificationsPlugin!.show(
      0,
      notificationTitle,
      notificationBody,
      platformChannelSpecifics,
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Study Plan'),
      ),
      body: Container(
        child: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              ElevatedButton(
                onPressed: _scheduleNotification,
                child: Text('Set Reminder'),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

This code sets up a basic user interface with a button to set a reminder. It also initializes the Flutter Local Notifications plugin and sets up the necessary notification settings.

## Conclusion

Congratulations! You have successfully implemented a study plan app with subject-specific reminders using Flutter Alarm Manager. With this app, you can now effectively manage your study time and stay organized. Feel free to enhance the app by adding more features and personalizing it to suit your needs. Happy studying!

---

#flutter #studyplan #alarmmanager #flutterlocalnotifications