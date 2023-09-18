---
layout: post
title: "Building a medication reminder app using Flutter Alarm Manager"
description: " "
date: 2023-09-18
tags: [MedicationReminderApp]
comments: true
share: true
---

In today's fast-paced world, it's easy to forget to take important medications regularly. However, with the advancements in mobile app development, we have the power to create a medication reminder app that keeps us on track with our medication schedules. In this blog post, we will explore how to build a medication reminder app using Flutter Alarm Manager.

## What is Flutter Alarm Manager?

Flutter Alarm Manager is a plugin that allows developers to schedule and manage alarms or reminders in Flutter applications. It provides an intuitive interface to set reminders at specific times, recurring intervals, or even at predetermined dates. With Flutter Alarm Manager, you can easily add medication reminders to your app and help users stay on top of their treatment plans.

## Getting Started

Before we dive into the code, make sure you have Flutter and Dart installed on your machine. If not, head over to the Flutter website (www.flutter.dev) for instructions on how to set up your development environment.

To get started, create a new Flutter project by running the following command:

```
flutter create medication_reminder_app
```

## Implementing Flutter Alarm Manager

To use Flutter Alarm Manager in our app, we need to include the `flutter_local_notifications` package in our `pubspec.yaml` file. Add the following line under the `dependencies` section:

```yaml
dependencies:
  flutter_local_notifications: ^2.0.0
```

Next, import the necessary packages in your Dart file:

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';
import 'package:flutter/material.dart';
```

Now, we can start building the UI of our medication reminder app. Create a stateful widget called `MedicationReminderApp`:

```dart
class MedicationReminderApp extends StatefulWidget {
  @override
  _MedicationReminderAppState createState() => _MedicationReminderAppState();
}

class _MedicationReminderAppState extends State<MedicationReminderApp> {
  FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin =
      FlutterLocalNotificationsPlugin();

  @override
  void initState() {
    super.initState();
    initializeNotifications();
  }

  Future<void> initializeNotifications() async {
    const AndroidInitializationSettings initializationSettingsAndroid =
        AndroidInitializationSettings('app_icon');
    final InitializationSettings initializationSettings =
        InitializationSettings(android: initializationSettingsAndroid);
    await flutterLocalNotificationsPlugin.initialize(initializationSettings);
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Medication Reminder App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Medication Reminder'),
        ),
        body: Center(
          child: Text('Build your medication reminder app UI here'),
        ),
      ),
    );
  }
}
```

In the above code, `initializeNotifications` initializes the Flutter Local Notifications plugin, and the `build` method sets up the basic UI structure of our app.

## Setting Medication Reminders

To set up medication reminders, we will add a widget called `MedicationReminderForm` within the `body` of our `Scaffold`. This widget will allow users to input their medication details and schedule reminders. 

```dart
class MedicationReminderForm extends StatefulWidget {
  @override
  _MedicationReminderFormState createState() => _MedicationReminderFormState();
}

class _MedicationReminderFormState extends State<MedicationReminderForm> {
  TimeOfDay selectedTime = TimeOfDay.now();

  Future<void> selectTime(BuildContext context) async {
    final TimeOfDay? pickedTime = await showTimePicker(
      context: context,
      initialTime: selectedTime,
    );

    if (pickedTime != null && pickedTime != selectedTime) {
      setState(() {
        selectedTime = pickedTime;
      });
    }
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        ListTile(
          title: Text('Medication Time: ${selectedTime.format(context)}'),
          trailing: Icon(Icons.edit),
          onTap: () => selectTime(context),
        ),
        ElevatedButton(
          onPressed: () => setMedicationReminder(selectedTime),
          child: Text('Set Reminder'),
        ),
      ],
    );
  }

  Future<void> setMedicationReminder(TimeOfDay timeOfDay) async {
    final DateTime now = DateTime.now();
    final DateTime scheduledTime = DateTime(
      now.year,
      now.month,
      now.day,
      timeOfDay.hour,
      timeOfDay.minute,
    );

    final AndroidNotificationDetails androidPlatformChannelSpecifics =
        AndroidNotificationDetails(
      'channel_id',
      'channel_name',
      'channel_description',
      priority: Priority.high,
      importance: Importance.max,
    );

    final NotificationDetails platformChannelSpecifics =
        NotificationDetails(android: androidPlatformChannelSpecifics);

    await flutterLocalNotificationsPlugin.zonedSchedule(
      0,
      'Medication Reminder',
      'Take your medication now!',
      scheduledTime,
      platformChannelSpecifics,
      uiLocalNotificationDateInterpretation:
          UILocalNotificationDateInterpretation.absoluteTime,
      androidAllowWhileIdle: true,
    );
  }
}
```

The above code shows the implementation of the `MedicationReminderForm`, which allows users to select a time for their medication reminder. It also sets up a notification using the `flutterLocalNotificationsPlugin.zonedSchedule` method. We pass in the reminder details such as title, message, scheduled time, and notification settings.

## Conclusion

In this blog post, we explored how to build a medication reminder app using the Flutter Alarm Manager plugin. We learned how to initialize the plugin, set up the basic UI structure, and schedule medication reminders using the Flutter Local Notifications package. With this knowledge, you can now create an app that helps individuals stay on track with their medication schedules.

Remember, staying consistent with medication is vital for one's health and well-being. By building a medication reminder app, you contribute to enhancing the overall healthcare experience and promoting healthier lifestyles.

## #Flutter #MedicationReminderApp