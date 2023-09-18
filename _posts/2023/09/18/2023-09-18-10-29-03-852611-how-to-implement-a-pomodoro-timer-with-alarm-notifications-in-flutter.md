---
layout: post
title: "How to implement a Pomodoro timer with alarm notifications in Flutter"
description: " "
date: 2023-09-18
tags: [pomodorotimer]
comments: true
share: true
---

Are you looking to boost your productivity and manage your time effectively? Implementing a Pomodoro Timer can help! In this tutorial, we will guide you through building a Pomodoro Timer app with alarm notifications using Flutter.

## Getting Started

To get started, make sure you have Flutter installed on your local machine. If you haven't installed Flutter yet, you can follow the official Flutter installation guide for your respective operating system.

## Setting up the Project

Create a new Flutter project by running the following command in your terminal:

```bash
flutter create pomodoro_timer
```

Once the project is created, navigate to the project directory by running:

```bash
cd pomodoro_timer
```

## Designing the User Interface

In the `lib` folder, open the `main.dart` file and replace the boilerplate code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(PomodoroTimerApp());
}

class PomodoroTimerApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Pomodoro Timer',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: PomodoroTimerScreen(),
    );
  }
}

class PomodoroTimerScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Pomodoro Timer'),
      ),
      body: Center(
        child: Text(
          'Pomodoro Timer Screen',
          style: TextStyle(fontSize: 24),
        ),
      ),
    );
  }
}
```

This sets up the basic structure of our Pomodoro Timer app with a simple screen displaying the app title.

## Implementing the Timer Logic

To implement the timer logic, we will be using the `flutter_countdown_timer` package. Add the package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_countdown_timer: ^2.0.0
```

Now, run `flutter pub get` to fetch the package and its dependencies.

Next, replace the code in `PomodoroTimerScreen` with the following:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_countdown_timer/flutter_countdown_timer.dart';

const int _pomodoroDurationSeconds = 1500; // 25 minutes

class PomodoroTimerScreen extends StatefulWidget {
  @override
  _PomodoroTimerScreenState createState() => _PomodoroTimerScreenState();
}

class _PomodoroTimerScreenState extends State<PomodoroTimerScreen> {
  int _currentTime = _pomodoroDurationSeconds;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Pomodoro Timer'),
      ),
      body: Center(
        child: CountdownTimer(
          endTime: _currentTime,
          widgetBuilder: (_, CurrentRemainingTime? time) {
            if (time == null) {
              return Text(
                'Time\'s up!',
                style: TextStyle(fontSize: 24),
              );
            }
            return Text(
              '${time.min}:${time.sec}',
              style: TextStyle(fontSize: 48),
            );
          },
        ),
      ),
    );
  }
}
```

The `PomodoroTimerScreen` widget now displays the countdown timer using the `CountdownTimer` widget from the `flutter_countdown_timer` package. The timer is set to the default Pomodoro duration of 25 minutes.

## Adding Alarm Notifications

To add alarm notifications when the timer ends, we will use the `flutter_local_notifications` package. Add the package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_countdown_timer: ^2.0.0
  flutter_local_notifications: ^9.0.0
```

Run `flutter pub get` to fetch the package and its dependencies.

Next, replace the code in `_PomodoroTimerScreenState` with the following:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_countdown_timer/flutter_countdown_timer.dart';
import 'package:flutter_local_notifications/flutter_local_notifications.dart';

class PomodoroTimerScreen extends StatefulWidget {
  @override
  _PomodoroTimerScreenState createState() => _PomodoroTimerScreenState();
}

class _PomodoroTimerScreenState extends State<PomodoroTimerScreen> {
  FlutterLocalNotificationsPlugin? _flutterLocalNotificationsPlugin;
  int _currentTime = _pomodoroDurationSeconds;
  bool _isTimerRunning = false;

  @override
  void initState() {
    super.initState();
    _initializeNotifications();
  }

  void _initializeNotifications() {
    _flutterLocalNotificationsPlugin = FlutterLocalNotificationsPlugin();

    const AndroidInitializationSettings initializationSettingsAndroid =
        AndroidInitializationSettings('app_icon');
    final InitializationSettings initializationSettings =
        InitializationSettings(android: initializationSettingsAndroid);

    _flutterLocalNotificationsPlugin!.initialize(initializationSettings,
        onSelectNotification: (String? payload) async {
      // Handle notification click event
      // ...
    });
  }

  void _showNotification() async {
    const AndroidNotificationDetails androidPlatformChannelSpecifics =
        AndroidNotificationDetails(
      'pomodoro_timer_channel',
      'Pomodoro Timer',
      'Notifications for Pomodoro Timer',
      importance: Importance.high,
      priority: Priority.high,
    );

    const NotificationDetails platformChannelSpecifics =
        NotificationDetails(android: androidPlatformChannelSpecifics);

    await _flutterLocalNotificationsPlugin!.show(
        0, 'Time\'s up!', 'Your Pomodoro session has ended.', platformChannelSpecifics);
  }

  void _startTimer() {
    setState(() {
      _isTimerRunning = true;
    });
  }

  void _stopTimer() {
    setState(() {
      _currentTime = _pomodoroDurationSeconds;
      _isTimerRunning = false;
      _showNotification();
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Pomodoro Timer'),
      ),
      body: Center(
        child: CountdownTimer(
          endTime: _currentTime,
          widgetBuilder: (_, CurrentRemainingTime? time) {
            if (time == null) {
              return Text(
                'Time\'s up!',
                style: TextStyle(fontSize: 24),
              );
            }
            return Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Text(
                  '${time.min.toString().padLeft(2, "0")}:${time.sec.toString().padLeft(2, "0")}',
                  style: TextStyle(fontSize: 48),
                ),
                SizedBox(height: 24),
                if (!_isTimerRunning)
                  ElevatedButton(
                    onPressed: _startTimer,
                    child: Text('Start Timer'),
                  )
                else
                  ElevatedButton(
                    onPressed: _stopTimer,
                    child: Text('Stop Timer'),
                  )
              ],
            );
          },
        ),
      ),
    );
  }
}
```

The `_PomodoroTimerScreenState` widget now initializes the `flutter_local_notifications` package and sets up notification channels. It also includes methods for showing the notification when the timer ends, starting and stopping the timer, and updating the UI accordingly.

## Conclusion

By following this tutorial, you have learned how to implement a Pomodoro Timer app with alarm notifications in Flutter. You can now customize the app UI, add additional features, or tweak the timer duration to suit your needs.

Remember to stay focused and take regular breaks to boost your productivity! Happy coding!

#flutter #pomodorotimer