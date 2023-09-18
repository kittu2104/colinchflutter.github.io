---
layout: post
title: "Creating a sleep quality tracker app with alarm functionality in Flutter"
description: " "
date: 2023-09-18
tags: [appdevelopment]
comments: true
share: true
---

In this tutorial, we will learn how to create a sleep quality tracker app with alarm functionality using Flutter. The app will allow users to track their sleep quality on a daily basis and set alarms for a better sleep routine. Flutter is a powerful cross-platform framework that allows us to build beautiful and interactive apps for iOS and Android.

## Prerequisites

Before getting started, make sure you have the following prerequisites installed on your system:

- Flutter SDK
- IDE of your choice (e.g. Android Studio, VS Code)

## Setting up the Project

To create a new Flutter project, open your terminal and run the following command:

```bash
flutter create sleep_tracker_app
```

This will create a new Flutter project named "sleep_tracker_app". Navigate to the project directory using the following command:

```bash
cd sleep_tracker_app
```

## Designing the User Interface

First, we need to design the user interface for our sleep tracker app. Open the `lib/main.dart` file in your preferred IDE and replace the default code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(SleepTrackerApp());
}

class SleepTrackerApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Sleep Tracker',
      theme: ThemeData(primarySwatch: Colors.blue),
      home: SleepTrackerHomePage(),
    );
  }
}

class SleepTrackerHomePage extends StatefulWidget {
  @override
  _SleepTrackerHomePageState createState() => _SleepTrackerHomePageState();
}

class _SleepTrackerHomePageState extends State<SleepTrackerHomePage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Sleep Tracker'),
      ),
      body: Center(
        child: Text(
          'Sleep Tracker Home Page',
          style: TextStyle(fontSize: 20),
        ),
      ),
    );
  }
}
```

This sets up the basic structure of our app. We have created a `SleepTrackerHomePage` widget as the home screen of our app and added it to the `MaterialApp` widget.

## Adding Sleep Tracking Functionality

To track sleep quality, we can use the `flutter_datetime_picker` package. Open the `pubspec.yaml` file and add the package in the dependencies section:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_datetime_picker: ^1.5.1
```

Save the file, and run the following command in the terminal to fetch the package:

```bash
flutter pub get
```

Now, modify the `_SleepTrackerHomePageState` widget as follows:

```dart
import 'package:flutter_datetime_picker/flutter_datetime_picker.dart';

class _SleepTrackerHomePageState extends State<SleepTrackerHomePage> {
  String selectedDate = '';

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Sleep Tracker'),
      ),
      body: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: [
          FlatButton(
            onPressed: () {
              DatePicker.showDatePicker(
                context,
                showTitleActions: true,
                onConfirm: (date) {
                  setState(() {
                    selectedDate = date.toString();
                  });
                },
                currentTime: DateTime.now(),
              );
            },
            child: Text('Select Sleep Date'),
          ),
          SizedBox(height: 20),
          Text(
            'Selected Date: $selectedDate',
            style: TextStyle(fontSize: 20),
          ),
        ],
      ),
    );
  }
}
```

In the code above, we added a `FlatButton` widget that allows the user to select the sleep date. When the user taps on the button, the `DatePicker` dialog will appear, and the selected date will be stored in the `selectedDate` variable.

## Adding Alarm Functionality

To provide alarm functionality, we can use the `flutter_local_notifications` package. Open the `pubspec.yaml` file and add the package in the dependencies section:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_datetime_picker: ^1.5.1
  flutter_local_notifications: ^3.0.3
```

Save the file and run the following command in the terminal to fetch the package:

```bash
flutter pub get
```

Now, modify the `_SleepTrackerHomePageState` widget as follows:

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';

class _SleepTrackerHomePageState extends State<SleepTrackerHomePage> {
  FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin =
      FlutterLocalNotificationsPlugin();

  @override
  void initState() {
    super.initState();
    initializeNotifications();
  }

  Future<void> initializeNotifications() async {
    var initializationSettingsAndroid =
        AndroidInitializationSettings('@mipmap/ic_launcher');
    var initializationSettingsIOS = IOSInitializationSettings();
    var initializationSettings = InitializationSettings(
        android: initializationSettingsAndroid, iOS: initializationSettingsIOS);
    await flutterLocalNotificationsPlugin.initialize(initializationSettings,
        onSelectNotification: onSelectNotification);
  }

  Future<void> onSelectNotification(String payload) async {
    if (payload != null) {
      debugPrint('Notification payload: $payload');
    }
  }

  Future<void> scheduleNotification(DateTime dateTime) async {
    var androidPlatformChannelSpecifics = AndroidNotificationDetails(
      'channel_id',
      'channel_name',
      'channel_description',
      importance: Importance.max,
      priority: Priority.high,
    );
    var iOSPlatformChannelSpecifics = IOSNotificationDetails();
    var platformChannelSpecifics = NotificationDetails(
        android: androidPlatformChannelSpecifics,
        iOS: iOSPlatformChannelSpecifics);

    await flutterLocalNotificationsPlugin.schedule(
      0,
      'Sleep Tracker Alarm',
      'Wake up! It\'s time to start your day.',
      dateTime,
      platformChannelSpecifics,
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Sleep Tracker'),
      ),
      body: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: [
          FlatButton(
            onPressed: () {
              DatePicker.showDateTimePicker(
                context,
                showTitleActions: true,
                onConfirm: (date) {
                  setState(() {
                    scheduleNotification(date);
                  });
                },
                currentTime: DateTime.now(),
              );
            },
            child: Text('Set Alarm'),
          ),
        ],
      ),
    );
  }
}
```

In the code above, we have added alarm functionality using the `flutter_local_notifications` package. We initialize the notifications plugin and set up the necessary platform-specific settings. The `scheduleNotification` method schedules a notification with the provided date and time.

## Running the App

Now that we have completed the implementation, we can run the app on either an emulator or connected device. Make sure your emulator or device is running, and execute the following command in the terminal:

```bash
flutter run
```

The app will launch on the device, and you can start tracking your sleep quality and setting alarms for a better sleep routine!

## Conclusion

In this tutorial, we learned how to create a sleep quality tracker app with alarm functionality using Flutter. We designed the user interface, added sleep tracking functionality, and integrated alarm functionality using Flutter packages. Flutter's versatility allows us to create powerful and feature-rich apps easily. You can further enhance the app by adding more features such as sleep analysis and data visualization.

#flutter #appdevelopment