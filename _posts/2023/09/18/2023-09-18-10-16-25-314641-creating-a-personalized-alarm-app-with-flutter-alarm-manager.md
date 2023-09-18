---
layout: post
title: "Creating a personalized alarm app with Flutter Alarm Manager"
description: " "
date: 2023-09-18
tags: [AlarmApp]
comments: true
share: true
---

In today's fast-paced world, it can be easy to forget important tasks or appointments. That's where alarm apps come in handy. And what's better than having a personalized alarm app that you can customize to your liking? In this tutorial, we will explore how to create a personalized alarm app using Flutter Alarm Manager plugin.

## What is Flutter Alarm Manager?
[Flutter Alarm Manager](https://pub.dev/packages/flutter_alarm_manager) is a Flutter plugin that allows you to schedule and manage alarms in your Flutter app. It provides a simple and intuitive API to create, update, and delete alarms. With Flutter Alarm Manager, you can schedule one-time alarms, recurring alarms, and even alarms that trigger at specific intervals.

## Prerequisites
Before we dive into building our personalized alarm app, make sure you have Flutter and Dart installed on your machine. You can download and install them from the official Flutter website.

## Getting Started
To start, create a new Flutter project by running the following command in your terminal:
```bash
flutter create personalized_alarm_app
```

Once the project is created, navigate to the project directory and open the `pubspec.yaml` file. Add the `flutter_alarm_manager` dependency:
```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_alarm_manager: ^0.5.0
```

Save the file and run the following command to download the dependencies:
```bash
flutter pub get
```

## Designing the Alarm Screen
Let's begin by designing the alarm screen. Open the `lib/main.dart` file and replace the default content with the following code:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(PersonalizedAlarmApp());
}

class PersonalizedAlarmApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Personalized Alarm App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: AlarmScreen(),
    );
  }
}

class AlarmScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Personalized Alarm App'),
      ),
      body: Center(
        child: Text(
          'Welcome to the Alarm App!',
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

Save the file and run the app using the following command:
```bash
flutter run
```

You should see a basic alarm screen with an app bar and a centered text widget displaying "Welcome to the Alarm App!".

## Adding Alarm Functionality
Now that we have our basic alarm screen set up, let's add the alarm functionality. Replace the contents of the `AlarmScreen` class with the following code:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_alarm_manager/flutter_alarm_manager.dart';

class AlarmScreen extends StatefulWidget {
  @override
  _AlarmScreenState createState() => _AlarmScreenState();
}

class _AlarmScreenState extends State<AlarmScreen> {
  TextEditingController _controller;

  @override
  void initState() {
    super.initState();
    _controller = TextEditingController();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Personalized Alarm App'),
      ),
      body: Column(
        children: [
          TextField(
            controller: _controller,
            decoration: InputDecoration(
              labelText: 'Set Alarm',
            ),
          ),
          ElevatedButton(
            onPressed: () {
              _scheduleAlarm();
            },
            child: Text('Set Alarm'),
          ),
        ],
      ),
    );
  }

  void _scheduleAlarm() {
    String alarmTime = _controller.text;
    // Schedule the alarm using Flutter Alarm Manager API
    FlutterAlarmManager.scheduleAlarm(
      DateTime.now().add(Duration(minutes: 1)),
      (int id) {
        _showAlarmDialog();
      },
    );
  }

  void _showAlarmDialog() {
    showDialog(
      context: context,
      builder: (BuildContext context) {
        return AlertDialog(
          title: Text('Alarm'),
          content: Text('Wake up! It\'s time!'),
          actions: [
            TextButton(
              child: Text('Dismiss'),
              onPressed: () {
                Navigator.of(context).pop();
              },
            ),
          ],
        );
      },
    );
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }
}
```

In this code, we've added a text field and a button to set the alarm time. When the button is pressed, the `_scheduleAlarm` method is called, which schedules the alarm using the `FlutterAlarmManager` API. It sets the alarm to trigger after one minute for the sake of demonstration. When the alarm goes off, the `_showAlarmDialog` method is called, which displays an alert dialog.

Save the file and run the app again using the command `flutter run`. Try setting an alarm and see the alert dialog appear after one minute.

## Wrapping Up
In this tutorial, we have learned how to create a personalized alarm app using the Flutter Alarm Manager plugin. We designed a basic alarm screen and added functionality to schedule and trigger alarms. You can further enhance the app by allowing users to set custom alarm times and adding additional features like snooze and repeat options.

Remember to experiment and explore more features offered by the Flutter Alarm Manager plugin to create an alarm app that suits your needs!

#Flutter #AlarmApp