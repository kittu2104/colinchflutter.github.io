---
layout: post
title: "How to cancel or update alarms in Flutter using Alarm Manager"
description: " "
date: 2023-09-18
tags: [alarmmanager]
comments: true
share: true
---

In Flutter, you can schedule alarms and receive callbacks when the alarms fire using the `alarm_manager` package. This allows you to perform tasks at a specific time, even if your app is not running. However, there may be scenarios where you need to cancel or update an existing alarm. In this tutorial, we will learn how to cancel or update alarms using the `alarm_manager` package.

## Installation
First, you need to add the `alarm_manager` package to your `pubspec.yaml` file:

```yaml
dependencies:
  alarm_manager: ^0.4.0
```

Then, run the following command to fetch the package:

```bash
flutter pub get
```

## Scheduling an Alarm
To schedule an alarm, you can use the `AlarmManager` class provided by the `alarm_manager` package. Here's an example of how to schedule a simple alarm:

```dart
import 'package:alarm_manager/alarm_manager.dart';
import 'package:android_intent/android_intent.dart';

void scheduleAlarm() {
  var alarmTime = DateTime.now().add(Duration(minutes: 5));

  AlarmManager.oneShot(
    alarmTime,
    0,
    () {
      // Handle alarm callback
      print('Alarm fired!');
      // Perform your task here
    },
  );
}
```

In this example, we schedule an alarm to fire 5 minutes from the current time. When the alarm fires, the callback function is invoked, where you can perform your desired task.

## Canceling an Alarm
To cancel an alarm, you need to provide the same request code that was used to schedule the alarm. Here's an example of how to cancel a scheduled alarm:

```dart
void cancelAlarm() {
  AlarmManager.cancel(0); // Example request code
}
```

In this example, we cancel the alarm with request code `0`. Make sure to provide the correct request code for the alarm you want to cancel.

## Updating an Existing Alarm
To update an existing alarm, you can simply schedule a new alarm with the same request code as the one you want to update. This will automatically replace the existing alarm with the new one. Here's an example of how to update an alarm:

```dart
void updateAlarm() {
  var updatedTime = DateTime.now().add(Duration(minutes: 10));

  AlarmManager.oneShot(
    updatedTime,
    0, // Example request code
    () {
      // Handle alarm callback
      print('Updated alarm fired!');
      // Perform your updated task here
    },
  );
}
```

In this example, we update the alarm with request code `0` to fire 10 minutes from the current time. The previous alarm with the same request code will be replaced automatically.

## Conclusion
By using the `alarm_manager` package in Flutter, you can easily schedule alarms and receive callbacks at a specific time. Moreover, cancelling or updating existing alarms is straightforward. This provides flexibility in managing alarms within your Flutter application.

Remember to import the necessary packages and handle the required permissions, as described in the `alarm_manager` package documentation.

#flutter #alarmmanager