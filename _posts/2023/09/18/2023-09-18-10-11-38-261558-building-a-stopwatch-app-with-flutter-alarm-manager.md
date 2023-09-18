---
layout: post
title: "Building a stopwatch app with Flutter Alarm Manager"
description: " "
date: 2023-09-18
tags: [flutterdevelopment]
comments: true
share: true
---

In this tutorial, we will be building a stopwatch app using Flutter and the Alarm Manager library. Flutter is an open-source UI framework developed by Google, which allows developers to build beautiful and native-looking apps for mobile, web, and desktop platforms.

## Prerequisites

Before we begin, make sure you have Flutter installed on your machine. You can follow the official documentation to set up Flutter: [https://flutter.dev/docs/get-started/install](https://flutter.dev/docs/get-started/install)

## Setting up the project

1. Start by creating a new Flutter project using the following command:

```bash
flutter create stopwatch_app
```

2. Open the `pubspec.yaml` file and add the `alarm_manager` package dependency:

```yaml
dependencies:
  flutter:
    sdk: flutter
  alarm_manager: ^0.6.0
```

3. Save the file and run the following command to install the dependencies:

```bash
flutter pub get
```

## Creating the Stopwatch UI

1. Open `lib/main.dart` and replace the existing code with the following code:

```dart
import 'package:flutter/material.dart';
import 'package:alarm_manager/alarm_manager.dart';

void main() {
  runApp(StopwatchApp());
}

class StopwatchApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Stopwatch App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: StopwatchScreen(),
    );
  }
}

class StopwatchScreen extends StatefulWidget {
  @override
  _StopwatchScreenState createState() => _StopwatchScreenState();
}

class _StopwatchScreenState extends State<StopwatchScreen> {
  int milliseconds = 0;
  bool isRunning = false;
  Timer? timer;

  void startTimer() {
    timer = Timer.periodic(Duration(milliseconds: 100), (Timer t) {
      setState(() {
        milliseconds += 100;
      });
    });
  }

  void stopTimer() {
    if (timer != null) {
      timer!.cancel();
      timer = null;
    }
  }

  void resetTimer() {
    setState(() {
      milliseconds = 0;
    });
  }

  void handleStartStopButtonPressed() {
    setState(() {
      isRunning = !isRunning;
      if (isRunning) {
        startTimer();
        AlarmManager.periodic(onAlarm: () {
          // Perform any background task here
        }, interval: 1000);
      } else {
        stopTimer();
        AlarmManager.cancel();
      }
    });
  }

  @override
  void dispose() {
    stopTimer();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    String formattedTime = formatTime(milliseconds);
    return Scaffold(
      appBar: AppBar(
        title: Text('Stopwatch App'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text(
              formattedTime,
              style: TextStyle(fontSize: 48),
            ),
            SizedBox(height: 16),
            RaisedButton(
              onPressed: handleStartStopButtonPressed,
              child: Text(
                isRunning ? 'Stop' : 'Start',
              ),
            ),
            SizedBox(height: 16),
            RaisedButton(
              onPressed: resetTimer,
              child: Text('Reset'),
            ),
          ],
        ),
      ),
    );
  }

  String formatTime(int milliseconds) {
    int minutes = milliseconds ~/ 60000;
    int seconds = (milliseconds % 60000) ~/ 1000;
    int hundredths = (milliseconds % 1000) ~/ 10;
    return '${minutes.toString().padLeft(2, '0')}:${seconds.toString().padLeft(2, '0')}.${hundredths.toString().padLeft(2, '0')}';
  }
}
```

This code sets up the basic structure of our stopwatch app, including a Start/Stop button and a Reset button.

2. Save the file and run the app using the following command:

```bash
flutter run
```

## Conclusion

In this tutorial, we built a stopwatch app using Flutter and the Alarm Manager library. We created a simple UI with a Start/Stop button and a Reset button, and implemented the stopwatch functionality using the Timer class. Alarm Manager was used to periodically execute a background task while the stopwatch is running. Feel free to enhance the app further by adding features like lap timings or customizations.

Stay tuned for more Flutter tutorials!

#flutter #flutterdevelopment