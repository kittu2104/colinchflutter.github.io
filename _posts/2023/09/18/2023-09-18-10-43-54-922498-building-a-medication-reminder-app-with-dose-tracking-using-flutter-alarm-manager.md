---
layout: post
title: "Building a medication reminder app with dose tracking using Flutter Alarm Manager"
description: " "
date: 2023-09-18
tags: [appdevelopment]
comments: true
share: true
---

In this tutorial, we will build a medication reminder app using Flutter and Flutter Alarm Manager. With this app, users will be able to set reminders for taking their medications and track their dosage schedule. Flutter Alarm Manager will help us manage and schedule the reminders effectively.

## What is Flutter Alarm Manager?

[Flutter Alarm Manager](https://pub.dev/packages/flutter_local_notifications) is a Flutter plugin that allows you to schedule and manage alarms, notifications, and reminders in your app. It provides a flexible and easy-to-use interface for setting up notifications and executing tasks based on time-based events.

## Prerequisites

To follow along with this tutorial, you should have the following prerequisites:

- Flutter SDK installed on your machine
- Android Studio or any other IDE of your choice
- Basic understanding of Flutter and Dart programming language

## Setting Up the Project

1. Create a new Flutter project using the following command:

```dart
flutter create medication_reminder_app
```

2. Open the project in your preferred IDE.

3. Add the following dependency to your `pubspec.yaml` file:

```dart
dependencies:
  flutter_local_notifications: ^7.1.1
```

4. Run the following command in the terminal to install the dependency:

```dart
flutter pub get
```

## Creating the Reminder Screen

1. Open the `lib/main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_local_notifications/flutter_local_notifications.dart';

final FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin =
    FlutterLocalNotificationsPlugin();

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  const AndroidInitializationSettings initializationSettingsAndroid =
      AndroidInitializationSettings('app_icon');
  final InitializationSettings initializationSettings = InitializationSettings(
    android: initializationSettingsAndroid,
  );
  await flutterLocalNotificationsPlugin.initialize(initializationSettings);
  runApp(MedicationReminderApp());
}

class MedicationReminderApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Medication Reminder',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: ReminderScreen(),
    );
  }
}

class ReminderScreen extends StatefulWidget {
  @override
  _ReminderScreenState createState() => _ReminderScreenState();
}

class _ReminderScreenState extends State<ReminderScreen> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Medication Reminder'),
      ),
      body: Center(
        child: Text('Welcome to Medication Reminder App!'),
      ),
    );
  }
}
```

2. Save the file and run the app using the following command:

```dart
flutter run
```

3. The app will open with a simple screen displaying the text "Welcome to Medication Reminder App!".

## Integrating Flutter Alarm Manager

1. Open the `lib/main.dart` file and modify the `_ReminderScreenState` class as follows:

```dart
class _ReminderScreenState extends State<ReminderScreen> {
  FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin;

  @override
  void initState() {
    super.initState();
    flutterLocalNotificationsPlugin = FlutterLocalNotificationsPlugin();

    final initializationSettingsAndroid = AndroidInitializationSettings('app_icon');
    final initializationSettings =
        InitializationSettings(android: initializationSettingsAndroid);
    flutterLocalNotificationsPlugin.initialize(initializationSettings);
  }

  Future<void> _scheduleNotification() async {
    var scheduledNotificationDateTime = DateTime.now().add(Duration(seconds: 5));

    var androidPlatformChannelSpecifics = AndroidNotificationDetails(
        'channel id',
        'channel name',
        'channel description',
        icon: 'app_icon',
        sound: RawResourceAndroidNotificationSound('notification_sound'),
        largeIcon: DrawableResourceAndroidBitmap('app_icon'));

    var platformChannelSpecifics =
        NotificationDetails(android: androidPlatformChannelSpecifics);

    await flutterLocalNotificationsPlugin.schedule(
      0,
      'Medication Reminder',
      'Time to take your medication!',
      scheduledNotificationDateTime,
      platformChannelSpecifics,
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Medication Reminder'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text('Welcome to Medication Reminder App!'),
            RaisedButton(
              onPressed: _scheduleNotification,
              child: Text('Set Medication Reminder'),
            ),
          ],
        ),
      ),
    );
  }
}
```

2. Save the file and run the app again.

3. Clicking the "Set Medication Reminder" button will now schedule a notification to be displayed after 5 seconds.

Congratulations! You have successfully built a medication reminder app with dose tracking using Flutter Alarm Manager. You can now enhance the app by allowing users to set custom reminders and track their medication dosage schedule.

#flutter #appdevelopment