---
layout: post
title: "Creating a countdown timer with Flutter Alarm Manager"
description: " "
date: 2023-09-18
tags: []
comments: true
share: true
---

Flutter is a cross-platform framework that allows developers to write applications for iOS, Android, and the web using a single codebase. In this tutorial, we will learn how to create a countdown timer using Flutter Alarm Manager plugin. The countdown timer can be used in various applications, from productivity apps to games.

## Getting Started

Before we begin, make sure you have Flutter and Dart installed on your machine. If not, follow the official Flutter installation guide to set up your environment. Additionally, you will need to add the Flutter Alarm Manager plugin to your Flutter project. You can do this by adding the following dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_alarm_manager: ^1.0.0
```

Once you have added the dependency, run `flutter pub get` to fetch the plugin into your project.

## Implementing the Countdown Timer

To create a countdown timer, we need to define the duration for the timer and display it in our Flutter app. Here's the code to implement a simple countdown timer:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_alarm_manager/flutter_alarm_manager.dart';

void main() {
  runApp(CountdownTimerApp());
}

class CountdownTimerApp extends StatefulWidget {
  @override
  _CountdownTimerAppState createState() => _CountdownTimerAppState();
}

class _CountdownTimerAppState extends State<CountdownTimerApp> {
  Duration _duration = Duration(minutes: 5);
  DateTime _endTime;

  @override
  void initState() {
    super.initState();

    _endTime = DateTime.now().add(_duration);
    _scheduleTimer();
  }

  void _scheduleTimer() {
    AlarmManager.oneShotAt(_endTime, onTimerEnd);
  }

  void onTimerEnd() {
    print('Timer ended!');
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Countdown Timer',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Countdown Timer'),
        ),
        body: Center(
          child: StreamBuilder(
            stream: Stream.periodic(Duration(seconds: 1), (i) =>
                _endTime.difference(DateTime.now())),
            builder: (context, snapshot) {
              if (snapshot.hasError) {
                return Text('Error: ${snapshot.error}');
              }
              if (snapshot.connectionState == ConnectionState.waiting) {
                return CircularProgressIndicator();
              }
              final remainingTime = snapshot.data;

              if (remainingTime.isNegative) {
                return Text('Timer ended!');
              }

              return Text(
                '${remainingTime.inMinutes}:${remainingTime.inSeconds.remainder(60)}',
                style: TextStyle(fontSize: 48),
              );
            },
          ),
        ),
      ),
    );
  }
}
```

The `CountdownTimerApp` class extends the `StatefulWidget` class and defines the state for our countdown timer. The `_duration` variable determines the duration of the countdown timer, which is set to 5 minutes in this example. The `_endTime` variable is calculated by adding the current time to the duration.

In the `initState()` method, we set the `_endTime` variable and schedule the timer using the `AlarmManager.oneShotAt()` method provided by the Flutter Alarm Manager plugin. We specify the `_endTime` as the trigger time for the timer and the `onTimerEnd` callback function to be executed when the timer ends.

In the `build()` method, we create a `StreamBuilder` widget that updates every second and calculates the remaining time by subtracting the current time from the `_endTime`. We then display the remaining time in the format `mm:ss` using the `Text` widget.

## Conclusion

In this tutorial, we learned how to create a countdown timer using the Flutter Alarm Manager plugin. We explored how to schedule the timer and update its UI in real-time. You can build upon this example to add more functionality, such as starting and stopping the timer, or customizing the UI.

Remember to import the Flutter Alarm Manager package, schedule the timer using `AlarmManager.oneShotAt()`, and update the UI using a `StreamBuilder`.