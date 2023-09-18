---
layout: post
title: "Implementing a water reminder app using Flutter Alarm Manager"
description: " "
date: 2023-09-18
tags: [mobileapp]
comments: true
share: true
---

In today's busy and fast-paced world, it's easy to forget to stay hydrated throughout the day. But with the help of technology, we can create a water reminder app to remind us to drink water at regular intervals. In this tutorial, we will be using the Flutter Alarm Manager package to implement this app.

## Prerequisites

Before we begin, make sure you have Flutter installed on your machine. You can download and install Flutter by following the official documentation: [Flutter Installation Guide](https://flutter.dev/docs/get-started/install)

## Setting up the Flutter Alarm Manager Package

To get started, create a new Flutter project and open it in your favorite code editor. Then, add the following dependency to your `pubspec.yaml` file:

```dart
dependencies:
  flutter:
    sdk: flutter
  flutter_alarm_manager: ^0.4.3
```

Save the file and run `flutter packages get` in the terminal to install the package.

## Creating the Water Reminder App

Now, let's create the basic structure of our app. Open the `lib/main.dart` file and replace the default code with the following:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_alarm_manager/flutter_alarm_manager.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Water Reminder',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: HomePage(),
    );
  }
}

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Water Reminder'),
      ),
      body: Center(
        child: RaisedButton(
          child: Text('Set Reminder'),
          onPressed: () {
            _setReminder();
          },
        ),
      ),
    );
  }

  void _setReminder() {
    FlutterAlarmManager.periodic(
      Duration(minutes: 60), // Remind every 60 minutes
      0, // Unique ID for the alarm
      _showNotification, // Callback function
    );
  }

  void _showNotification() {
    // TODO: Implement notification logic
  }
}
```

This code sets up a basic Flutter app with a single button that, when pressed, calls the `_setReminder` function. Inside the `_setReminder` function, we use the `FlutterAlarmManager.periodic` method to schedule a periodic reminder every 60 minutes. The `_showNotification` function will be called each time the reminder triggers.

## Implementing the Notification Logic

To complete our water reminder app, we need to implement the notification logic inside the `_showNotification` function. We will be using the `flutter_local_notifications` package to show the notifications. Add the following dependency to your `pubspec.yaml` file:

```dart
dependencies:
  flutter_local_notifications: ^5.0.0
```

Save the file and run `flutter packages get` to install the package.

Next, open the `lib/main.dart` file and add the following import statement below the existing import statements:

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';
```

Now, let's modify the `_showNotification` function as follows:

```dart
void _showNotification() async {
  FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin =
      FlutterLocalNotificationsPlugin();
      
  const AndroidInitializationSettings initializationSettingsAndroid =
      AndroidInitializationSettings('app_icon');

  final IOSInitializationSettings initializationSettingsIOS =
      IOSInitializationSettings(
    onDidReceiveLocalNotification: (int id, String title, String body, String payload) async {
      // TODO: Handle received notification
    },
  );

  final InitializationSettings initializationSettings = InitializationSettings(
    android: initializationSettingsAndroid, ios: initializationSettingsIOS
  );

  await flutterLocalNotificationsPlugin.initialize(initializationSettings);
  
  const AndroidNotificationDetails androidPlatformChannelSpecifics =
      AndroidNotificationDetails('water_reminder', 'Water Reminder',
          'Reminds you to drink water at regular intervals',
          importance: Importance.high);

  const NotificationDetails platformChannelSpecifics =
      NotificationDetails(android: androidPlatformChannelSpecifics);

  await flutterLocalNotificationsPlugin.show(
    0, // Unique ID for the notification
    'Drink Water', // Notification title
    'Remember to stay hydrated!', // Notification body
    platformChannelSpecifics,
    payload: 'reminder', // Payload for future use
  );
}
```

In this updated code, we initialize the `flutterLocalNotificationsPlugin` and set up the Android and iOS initialization settings. We then call the `flutterLocalNotificationsPlugin.show` method to display the notification with a custom title and body.

## Running the App

To run the app, connect your device or start an emulator, and run the following command in the terminal:

```
flutter run
```

You should see the Water Reminder app with a button labeled "Set Reminder". Clicking the button will schedule a periodic reminder, and you should receive a notification every 60 minutes reminding you to drink water.

## Conclusion

In this tutorial, we learned how to implement a water reminder app using the Flutter Alarm Manager package. We also added notification functionality using the flutter_local_notifications package. With this knowledge, you can now build your own reminder apps with customized notification features. Don't forget to stay hydrated!

#flutter #mobileapp #waterreminder #flutteralarmmanager