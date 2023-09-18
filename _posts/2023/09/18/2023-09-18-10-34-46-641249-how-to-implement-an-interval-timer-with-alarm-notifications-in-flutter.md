---
layout: post
title: "How to implement an interval timer with alarm notifications in Flutter"
description: " "
date: 2023-09-18
tags: [intervalTimer]
comments: true
share: true
---

If you are developing a mobile application with Flutter and want to implement an interval timer with alarm notifications, you've come to the right place! In this tutorial, we will guide you through the process of creating a simple interval timer app that allows users to set custom intervals and receive alarm notifications when each interval ends.

## Step 1: Setting up the Project

First, make sure you have Flutter installed on your machine. You can check if Flutter is properly installed by running `flutter doctor` in your terminal.

Create a new Flutter project by running the following command:

```
flutter create interval_timer_app
cd interval_timer_app
```

Open the project in your favorite code editor.

## Step 2: Adding Dependencies

To implement the interval timer and alarm notifications functionality, we will be using the `audioplayers` and `flutter_local_notifications` packages. Open the `pubspec.yaml` file and add the following dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter
  audioplayers: ^0.18.3
  flutter_local_notifications: ^8.2.0
```

Save the file and run `flutter pub get` to fetch the dependencies.

## Step 3: Creating the Timer Page

Create a new Dart file called `timer_page.dart` with the following code:

```dart
import 'package:flutter/material.dart';
import 'package:audioplayers/audioplayers.dart';

class TimerPage extends StatefulWidget {
  @override
  _TimerPageState createState() => _TimerPageState();
}

class _TimerPageState extends State<TimerPage> {
  int minutes = 0;
  int seconds = 0;

  bool isRunning = false;
  bool isPaused = false;

  AudioCache audioCache = AudioCache();
  AudioPlayer player = AudioPlayer();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Interval Timer'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text(
              '$minutes:${seconds.toString().padLeft(2, '0')}',
              style: TextStyle(fontSize: 64),
            ),
            SizedBox(height: 32),
            ElevatedButton(
              onPressed: isRunning ? null : startTimer,
              child: Text('Start Timer'),
            ),
            SizedBox(height: 16),
            ElevatedButton(
              onPressed: isRunning && !isPaused ? pauseTimer : null,
              child: Text('Pause Timer'),
            ),
            SizedBox(height: 16),
            ElevatedButton(
              onPressed: isPaused ? resumeTimer : null,
              child: Text('Resume Timer'),
            ),
            SizedBox(height: 16),
            ElevatedButton(
              onPressed: isRunning ? null : resetTimer,
              child: Text('Reset Timer'),
            ),
          ],
        ),
      ),
    );
  }
  
  // Implement the timer functionality here
  ...
}
```

This code sets up the basic structure of our timer page. It includes a timer display, buttons to start, pause, resume, and reset the timer, and necessary variables and packages.

## Step 4: Implementing the Timer Functionality

In the `_TimerPageState` class, add the following methods to implement the timer functionality:

```dart
void startTimer() {
  if (!isRunning) {
    const oneSec = Duration(seconds: 1);
    Timer.periodic(oneSec, (Timer timer) {
      if (seconds < 59) {
        setState(() {
          seconds++;
        });
      } else {
        setState(() {
          seconds = 0;
          minutes++;
        });
      }
    });
    setState(() {
      isRunning = true;
    });
  }
}

void pauseTimer() {
  setState(() {
    isPaused = true;
  });
}

void resumeTimer() {
  setState(() {
    isPaused = false;
  });
}

void resetTimer() {
  if (isRunning) {
    setState(() {
      minutes = 0;
      seconds = 0;
      isRunning = false;
      isPaused = false;
    });
  }
}
```

These methods handle starting, pausing, resuming, and resetting the timer. The `startTimer` method uses a `Timer.periodic` function to update the seconds and minutes every second.

## Step 5: Adding Alarm Notifications

To add alarm notifications when the timer interval ends, we will use the `flutter_local_notifications` package. Add the following code to the `_TimerPageState` class:

```dart
void showNotification() async {
  const AndroidInitializationSettings initializationSettingsAndroid =
      AndroidInitializationSettings('app_icon');

  final InitializationSettings initializationSettings = InitializationSettings(
    android: initializationSettingsAndroid,
  );

  await flutterLocalNotificationsPlugin.initialize(initializationSettings);

  const AndroidNotificationDetails androidPlatformChannelSpecifics =
      AndroidNotificationDetails(
          'interval_timer_app_channel_id',
          'Interval Timer App Channel',
          'Channel for Interval Timer App',
          importance: Importance.max,
          priority: Priority.high);

  const NotificationDetails platformChannelSpecifics =
      NotificationDetails(android: androidPlatformChannelSpecifics);

  await flutterLocalNotificationsPlugin.show(
    0,
    'Interval Timer',
    'Interval ended',
    platformChannelSpecifics,
    payload: 'interval_ended',
  );
}
```

Make sure to import the necessary packages and initialize the `flutterLocalNotificationsPlugin` at the top of the file:

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';

final FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin =
    FlutterLocalNotificationsPlugin();
```

## Step 6: Triggering Alarm Notifications

To trigger the alarm notification when the interval ends, modify the `startTimer` method to include the following code:

```dart
void startTimer() {
  if (!isRunning) {
    const oneSec = Duration(seconds: 1);
    Timer.periodic(oneSec, (Timer timer) {
      if (!isPaused) {
        if (seconds < 59) {
          setState(() {
            seconds++;
          });
        } else {
          setState(() {
            seconds = 0;
            minutes++;
          });

          if (minutes == 5) {
            showNotification();
            // You can also play a sound here
          }
        }
      }
    });
    setState(() {
      isRunning = true;
    });
  }
}
```

In the `startTimer` method, we added a condition to check if the timer has reached 5 minutes (you can change this to a different interval as needed). When the condition is met, the `showNotification` method is called to trigger the notification.

## Step 7: Building and Running the App

To test the app, run the following command in your terminal:

```
flutter run
```

The app should launch on your connected device or emulator. Use the buttons to start, pause, resume, and reset the timer. After 5 minutes (or the set interval), an alarm notification should pop up.

Congratulations! You have successfully implemented an interval timer with alarm notifications in Flutter. Feel free to customize the UI or add more functionality as per your app's requirements.

#flutter #intervalTimer