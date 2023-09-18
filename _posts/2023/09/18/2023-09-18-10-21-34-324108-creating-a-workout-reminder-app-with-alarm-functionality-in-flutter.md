---
layout: post
title: "Creating a workout reminder app with alarm functionality in Flutter"
description: " "
date: 2023-09-18
tags: [AlarmApp]
comments: true
share: true
---

In today's fast-paced world, it can be challenging to stay committed to our workout routines. But with the help of technology, we can create an app that reminds us to exercise regularly. In this tutorial, we will explore how to build a workout reminder app with alarm functionality using Flutter.

## Getting Started

First, make sure you have Flutter installed on your machine. If you haven't already, follow the official Flutter installation guide for your operating system.

Once Flutter is set up, create a new Flutter project by running the following command:

```dart
flutter create workout_reminder_app
```

Navigate to the project directory:

```dart
cd workout_reminder_app
```

## Adding Required Dependencies

To implement the alarm functionality, we need to add two important dependencies to our `pubspec.yaml` file:

```yaml
dependencies:
  flutter_local_notifications: ^6.0.0
  timezone: ^0.7.0
```

The `flutter_local_notifications` package allows us to schedule and display local notifications on the user's device. The `timezone` package helps us handle time zone conversions accurately.

Run the following command to fetch the dependencies:

```dart
flutter pub get
```

## Creating the Reminder Page

Create a new Dart file, `reminder_page.dart`, in the `lib` directory. This file will serve as the main page of our app, where users can set their workout reminders. Here's a basic template for the `ReminderPage` class:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_local_notifications/flutter_local_notifications.dart';

class ReminderPage extends StatefulWidget {
  @override
  _ReminderPageState createState() => _ReminderPageState();
}

class _ReminderPageState extends State<ReminderPage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Workout Reminder'),
      ),
      body: Center(
        child: Text(
          'This is the reminder page',
          style: TextStyle(fontSize: 20),
        ),
      ),
    );
  }
}
```

## Adding Alarm Functionality

Inside the `_ReminderPageState` class, import `flutter_local_notifications` and define a function called `scheduleReminder`:

```dart
final FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin =
    FlutterLocalNotificationsPlugin();

Future<void> scheduleReminder() async {
  // TODO: Implement alarm functionality here
}
```

The `flutterLocalNotificationsPlugin` instance will allow us to schedule and display notifications. `scheduleReminder` will be responsible for setting up the alarm.

To schedule an alarm, we need to call the `flutterLocalNotificationsPlugin`'s `zonedSchedule` method. Here's an example implementation:

```dart
Future<void> scheduleReminder() async {
  await flutterLocalNotificationsPlugin.zonedSchedule(
    0,
    'Workout Reminder',
    'Time to exercise!',
    _nextInstanceOfExerciseTime(),
    const NotificationDetails(
      android: AndroidNotificationDetails(
        'workout_reminder_channel',
        'Workout Reminder',
        'Channel for workout reminders',
        importance: Importance.high,
      ),
    ),
    androidAllowWhileIdle: true,
    uiLocalNotificationDateInterpretation:
        UILocalNotificationDateInterpretation.absoluteTime,
  );
}

tz.TZDateTime _nextInstanceOfExerciseTime() {
  final tz.TZDateTime now = tz.TZDateTime.now(tz.local);
  tz.TZDateTime scheduledDate =
      tz.TZDateTime(tz.local, now.year, now.month, now.day, 18, 0);

  if (scheduledDate.isBefore(now)) {
    scheduledDate = scheduledDate.add(const Duration(days: 1));
  }

  return scheduledDate;
}
```

The `zonedSchedule` method takes various parameters, including an ID for the notification, a title, message, trigger time, notification details, and more. `_nextInstanceOfExerciseTime` function returns a `TZDateTime` object representing the next instance of a workout time (here, set to 6:00 PM).

## Adding User Interface

Now that our alarm functionality is in place, let's update the UI in the `ReminderPage` class. We will add a button that triggers the `scheduleReminder` function when pressed:

```dart
class _ReminderPageState extends State<ReminderPage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Workout Reminder'),
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: scheduleReminder,
          child: Text('Set Workout Reminder'),
        ),
      ),
    );
  }
}
```

## Testing the App

To test the app, run the following command:

```dart
flutter run
```

The app should launch on either an emulator or a physical device. Tap the "Set Workout Reminder" button to schedule the first workout reminder.

Congratulations! You have successfully created a workout reminder app with alarm functionality using Flutter. This app will help users stay committed to their fitness goals by reminding them to exercise regularly.

#Flutter #AlarmApp