---
layout: post
title: "Adding and managing multiple alarms with Flutter Alarm Manager"
description: " "
date: 2023-09-18
tags: [alarms]
comments: true
share: true
---

In mobile applications, there are often scenarios where you need to set and manage multiple alarms for different tasks or reminders. With the Flutter Alarm Manager plugin, you can easily add and handle multiple alarms in your Flutter app. In this blog post, we will walk you through the steps of setting up and managing multiple alarms using Flutter Alarm Manager plugin.

## Step 1: Setting up Flutter Alarm Manager

To get started, you need to add the `flutter_alarm_manager` dependency to your Flutter project. Open your `pubspec.yaml` file and add the following line under the `dependencies` section:

```
dependencies:
  flutter_alarm_manager: ^2.0.0
```

Then, save the file and run `flutter pub get` command to fetch the plugin from Dart packages.

## Step 2: Adding Alarms

To add alarms, you need to define the date and time for each alarm. You can use the `flutter_alarm_manager` plugin to schedule alarms at specific times. Here's an example of how to add multiple alarms:

```dart
import 'package:flutter_alarm_manager/flutter_alarm_manager.dart';

void addAlarm(DateTime time) {
  FlutterAlarmManager.schedule(
    id: time.millisecondsSinceEpoch.hashCode,
    scheduledDateTime: time,
    callback: alarmCallback,
    allowWhileIdle: true,
    exact: true,
    alarmClock: true,
    wakeup: true,
  );
}

void alarmCallback() {
  // Handle alarm event here
}

void main() {
  // add multiple alarms
  addAlarm(DateTime(2021, 12, 31, 8, 0, 0));
  addAlarm(DateTime(2022, 1, 1, 12, 0, 0));
  addAlarm(DateTime(2022, 2, 14, 9, 30, 0));
}
```

In the above code snippet, we define the `addAlarm` function that takes a `DateTime` parameter and uses the `FlutterAlarmManager.schedule` method to schedule an alarm. We generate a unique `id` for each alarm using the `hashCode` of the milliseconds since epoch value of the time. The `scheduledDateTime` is set to the specified time, and the `callback` method is called when the alarm triggers.

## Step 3: Managing Alarms

To manage alarms, you can retrieve a list of all scheduled alarms, cancel specific alarms, or clear all alarms. Here's an example of managing alarms:

```dart
import 'package:flutter_alarm_manager/flutter_alarm_manager.dart';

void getAllScheduledAlarms() {
  FlutterAlarmManager.getAll().then((alarms) {
    // Handle the list of alarms here
  });
}

void cancelAlarm(int id) {
  FlutterAlarmManager.cancel(id);
}

void cancelAllAlarms() {
  FlutterAlarmManager.cancelAll();
}

void main() {
  // get all scheduled alarms
  getAllScheduledAlarms();

  // cancel specific alarm
  cancelAlarm(123);

  // cancel all alarms
  cancelAllAlarms();
}
```

In the above code snippet, we define the `getAllScheduledAlarms` method to retrieve a list of all scheduled alarms, `cancelAlarm` to cancel a specific alarm using its `id`, and `cancelAllAlarms` to cancel all the scheduled alarms.

## Conclusion

By using the Flutter Alarm Manager plugin, you can easily add and manage multiple alarms in your Flutter application. You can schedule alarms at specific times, handle alarm events, and cancel or clear alarms as needed. This allows you to create time-sensitive reminders, notification systems, or other features that require alarm functionality in your app.

#flutter #alarms