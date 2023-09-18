---
layout: post
title: "Creating a calendar app with alarm functionality in Flutter"
description: " "
date: 2023-09-18
tags: []
comments: true
share: true
---

Flutter is a popular cross-platform development framework that allows developers to build robust applications for Android, iOS, and the web. In this tutorial, we will guide you through the process of creating a calendar app with alarm functionality using Flutter.

## Getting Started

To get started, make sure you have Flutter installed on your system. You can download and install Flutter by following the official Flutter documentation.

Once you have Flutter set up, create a new Flutter project by running the following command:

```dart
flutter create calendar_app
```

## Designing the User Interface

Before we dive into the code, let's design the user interface for our calendar app. We will use the `table_calendar` package to display the calendar and the `flutter_local_notifications` package to handle the alarm notifications.

First, add the required dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  table_calendar: ^3.0.4
  flutter_local_notifications: ^9.0.0
```

Next, replace the content of the `lib/main.dart` file with the following code:

```dart
import 'package:flutter/material.dart';
import 'package:table_calendar/table_calendar.dart';
import 'package:flutter_local_notifications/flutter_local_notifications.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Calendar App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: HomePage(),
    );
  }
}

class HomePage extends StatefulWidget {
  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  CalendarController _calendarController = CalendarController();

  FlutterLocalNotificationsPlugin _flutterLocalNotificationsPlugin =
      FlutterLocalNotificationsPlugin();

  @override
  void initState() {
    super.initState();
    _initializeNotifications();
  }

  void _initializeNotifications() async {
    var initializationSettingsAndroid =
        AndroidInitializationSettings('@mipmap/ic_launcher');
    var initializationSettingsIOS = IOSInitializationSettings();
    await _flutterLocalNotificationsPlugin.initialize(
        InitializationSettings(
            android: initializationSettingsAndroid,
            iOS: initializationSettingsIOS));
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Calendar App'),
      ),
      body: TableCalendar(
        calendarController: _calendarController,
        headerStyle: HeaderStyle(
          formatButtonTextStyle: TextStyle().copyWith(color: Colors.white),
          formatButtonDecoration: BoxDecoration(
            color: Colors.blue,
            borderRadius: BorderRadius.circular(20.0),
          ),
        ),
      ),
    );
  }
}
```

## Adding Alarm Functionality

To add alarm functionality to our calendar app, we need to handle the alarm notifications and schedule them based on user input. Let's update our `_HomePageState` class with the following changes:

```dart
class _HomePageState extends State<HomePage> {
  // Other code...

  void _scheduleAlarm(DateTime dateTime) async {
    var scheduledNotificationDateTime = dateTime.subtract(Duration(minutes: 5));
    var androidPlatformChannelSpecifics = AndroidNotificationDetails(
      'alarm_channel',
      'Alarm Channel',
      'Channel for alarms',
    );
    var iOSPlatformChannelSpecifics = IOSNotificationDetails();
    var platformChannelSpecifics = NotificationDetails(
      android: androidPlatformChannelSpecifics,
      iOS: iOSPlatformChannelSpecifics,
    );
    await _flutterLocalNotificationsPlugin.schedule(
      0,
      'Alarm',
      'It\'s time for your appointment!',
      scheduledNotificationDateTime,
      platformChannelSpecifics,
      payload: 'alarm',
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      // Other code...

      floatingActionButton: FloatingActionButton(
        onPressed: () {
          var selectedDay = _calendarController.selectedDay;
          _scheduleAlarm(selectedDay);
        },
        child: Icon(Icons.alarm),
      ),
    );
  }
}
```

In the above code, we added a `_scheduleAlarm` method that schedules the notification 5 minutes before the selected date. We also added a `FloatingActionButton` to the app bar that triggers the alarm scheduling when pressed.

## Conclusion

Congratulations! You have successfully created a calendar app with alarm functionality in Flutter. You can now customize the UI, add more features, and enhance the app further based on your requirements.

Remember to test your app thoroughly and consider handling edge cases such as permission handling for notifications.