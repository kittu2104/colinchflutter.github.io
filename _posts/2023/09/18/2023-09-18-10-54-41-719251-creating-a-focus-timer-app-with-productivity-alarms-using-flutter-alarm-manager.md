---
layout: post
title: "Creating a focus timer app with productivity alarms using Flutter Alarm Manager"
description: " "
date: 2023-09-18
tags: [tags]
comments: true
share: true
---

In today's fast-paced world, staying focused and productive can be a challenge. Luckily, technology can help us stay on track and achieve our goals. In this blog post, we will explore how to build a focus timer app with productivity alarms using Flutter Alarm Manager.

## What is Flutter Alarm Manager?

Flutter Alarm Manager is a powerful plugin that allows you to schedule alarms and manage them within your Flutter app. It provides a convenient way to set up reminders or notifications at specific times, helping users stay organized and productive.

## Building the Focus Timer App

To create our focus timer app, we will need to follow a few steps:

### Step 1: Set Up the Project

First, make sure you have Flutter and Dart installed on your machine. Create a new Flutter project using the following command:

```shell
flutter create focus_timer_app
cd focus_timer_app
```

### Step 2: Add Dependencies

Open the `pubspec.yaml` file and add the `flutter_alarm_manager` dependency:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_local_notifications: ^2.0.0
  flutter_alarm_manager: ^0.4.5
```

Then, run `flutter pub get` in your terminal to fetch the dependencies.

### Step 3: Design the User Interface

Create a new file `main.dart` and define the UI for your app. This can include a timer display, start/stop buttons, and notification settings. Use Flutter's widget system to build your user interface.

### Step 4: Implement the Timer Logic

In the `main.dart` file, define a StatefulWidget class called `FocusTimer`. This class will manage the timer logic and handle the start and stop actions.

```dart
class FocusTimer extends StatefulWidget {
  @override
  _FocusTimerState createState() => _FocusTimerState();
}

class _FocusTimerState extends State<FocusTimer> {
  Timer? _timer;
  int _secondsRemaining = 0;

  void startTimer() {
    // Start the timer logic
  }

  void stopTimer() {
    // Stop the timer logic
  }

  void resetTimer() {
    // Reset the timer logic
  }

  @override
  Widget build(BuildContext context) {
    // Build the UI for the timer app
  }
}
```

### Step 5: Utilize Flutter Alarm Manager

Using the Flutter Alarm Manager plugin, we can schedule alarms to trigger at specific times. In this case, we want to set an alarm to remind the user after a set amount of time has passed.

```dart
import 'package:flutter_alarm_manager/flutter_alarm_manager.dart';

void setProductivityAlarm() async {
  final now = DateTime.now();
  final timeDelay = const Duration(minutes: 25); // 25 minutes

  final scheduledTime = now.add(timeDelay);

  await FlutterAlarmManager.schedule(
    id: 0,
    scheduledDate: scheduledTime,
    callback: _handleProductivityAlarm,
  );
}

void _handleProductivityAlarm() {
  // Show a notification or perform any desired action when the alarm triggers
}
```

### Step 6: Connect the Timer and Alarms

In the `startTimer` method, call the `setProductivityAlarm` function to schedule the productivity alarm when the timer starts counting down. Likewise, cancel any existing alarms in the `stopTimer` method.

```dart
void startTimer() {
  // Start the timer logic
  setProductivityAlarm();
}

void stopTimer() {
  // Stop the timer logic
  FlutterAlarmManager.cancel(0);
}
```

### Step 7: Run the App

Finally, run the app using `flutter run` in your terminal and test the timer logic and productivity alarms.

## Conclusion

In this blog post, we learned how to create a focus timer app with productivity alarms using Flutter Alarm Manager. By combining the timer logic and alarm scheduling capabilities of the plugin, we can help users stay focused and productive. With Flutter's cross-platform capabilities, the app can be deployed to both iOS and Android devices. 

#tags: #Flutter #Productivity