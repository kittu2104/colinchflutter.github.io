---
layout: post
title: "Creating a goal tracker app with alarm notifications using Flutter Alarm Manager"
description: " "
date: 2023-09-18
tags: [GoalTrackerApp]
comments: true
share: true
---

![Goal Tracker App](https://example.com/goal-tracker-app.png)

In today's fast-paced world, managing and tracking goals has become more important than ever. That's why having a dedicated goal tracker app can help us stay organized and focused on achieving our goals. In this article, we will explore how to create a goal tracker app with alarm notifications using Flutter Alarm Manager.

## What is Flutter Alarm Manager?

Flutter Alarm Manager is a plugin that allows you to schedule alarms, notifications, and background services in your Flutter app. It works on both Android and iOS platforms, making it a versatile choice for implementing alarm and notification functionality.

## Setting up the Project

To begin building our goal tracker app, we need to set up a new Flutter project. Open your terminal, navigate to the desired directory, and run the following command:

```
flutter create goal_tracker_app
```

This will create a new Flutter project named `goal_tracker_app`. Once the project is created, navigate to the project directory:

```
cd goal_tracker_app
```

## Installing Dependencies

Next, we need to install the Flutter Alarm Manager plugin. Add the following line to the `dependencies` section of your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_alarm_manager: ^0.5.0
```

Save the file and run the following command to install the plugin:

```
flutter pub get
```

## Designing the User Interface

Now that our project is set up and the dependencies are installed, let's design the user interface for our goal tracker app. Open the `lib/main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(GoalTrackerApp());
}

class GoalTrackerApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Goal Tracker',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: GoalTrackerHomePage(),
    );
  }
}

class GoalTrackerHomePage extends StatefulWidget {
  @override
  _GoalTrackerHomePageState createState() => _GoalTrackerHomePageState();
}

class _GoalTrackerHomePageState extends State<GoalTrackerHomePage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Goal Tracker'),
      ),
      body: Center(
        child: Text(
          'Welcome to Goal Tracker App',
          style: TextStyle(fontSize: 24),
        ),
      ),
    );
  }
}
```

This sets up a basic Flutter app with a home page that displays a welcome message.

## Implementing Alarm Notifications

Now, let's add the functionality to schedule alarm notifications for our goals. In the `_GoalTrackerHomePageState` class, add the following code below the `build` method:

```dart
void _scheduleNotification() {
  // TODO: Implement alarm scheduling logic
}

@override
void initState() {
  super.initState();
  _scheduleNotification();
}
```

The `_scheduleNotification` method is where we will implement the logic to schedule the alarm notification. We will complete this method in the next step.

## Implementing Alarm Scheduling Logic

To schedule the alarm using Flutter Alarm Manager, we need to add the following code inside the `_scheduleNotification` method:

```dart
import 'package:flutter_alarm_manager/flutter_alarm_manager.dart';

void _scheduleNotification() async {
  final DateTime now = DateTime.now();
  final DateTime scheduledTime = now.add(Duration(minutes: 30));

  await FlutterAlarmManager.schedule(
    id: 0,
    title: 'Goal Tracker Reminder',
    body: 'Don\'t forget to work on your goals!',
    scheduledDate: scheduledTime,
    isExact: true,
    androidAllowWhileIdle: true,
  );
}
```

In this example code, we schedule an alarm notification 30 minutes from the current time. Feel free to customize the scheduling logic according to your requirements.

## Testing the App

To test the goal tracker app with alarm notifications, run the following command in your terminal:

```
flutter run
```

This will launch the app on the connected device or emulator. You should see the welcome message displayed on the home page, and an alarm notification will be scheduled as soon as the app runs.

![Goal Tracker Alarm Notification](https://example.com/goal-tracker-alarm-notification.png)

## Conclusion

In this article, we explored how to create a goal tracker app with alarm notifications using Flutter Alarm Manager. We covered setting up the project, installing dependencies, designing the user interface, and implementing alarm scheduling logic. Now, you have the foundation to build a powerful goal tracker app that keeps you on track and motivated towards achieving your goals.

#Flutter #GoalTrackerApp #AlarmNotifications