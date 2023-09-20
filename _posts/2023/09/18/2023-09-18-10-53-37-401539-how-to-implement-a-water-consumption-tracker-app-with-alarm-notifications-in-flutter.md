---
layout: post
title: "How to implement a water consumption tracker app with alarm notifications in Flutter"
description: " "
date: 2023-09-18
tags: [WaterTrackerApp]
comments: true
share: true
---

Are you looking for a convenient way to track your daily water consumption and stay hydrated? In this tutorial, we will walk you through the steps to implement a water consumption tracker app with alarm notifications using Flutter.

## Prerequisites

Before we begin, make sure you have Flutter installed on your computer. You can download and install Flutter by following the official documentation: [Flutter Installation](https://flutter.dev/docs/get-started/install)

## Step 1: Create a new Flutter Project

To create a new Flutter project, open your terminal and run the following command:

```shell
flutter create water_tracker_app
```

This will create a new directory named "water_tracker_app" containing all the necessary files for our app.

## Step 2: Set up Dependencies

Open the `pubspec.yaml` file in your project and add the following dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_local_notifications: ^[version]
```

Replace `[version]` with the latest version of the `flutter_local_notifications` package. This package allows us to display alarm notifications in our app.

After adding the dependencies, run the following command in your terminal:

```shell
flutter pub get
```

This will fetch and install the required packages into your project.

## Step 3: Implement the User Interface

Navigate to the `lib` directory and open the `main.dart` file. Replace the existing code with the following:

```dart
import 'package:flutter/material.dart';

void main() => runApp(WaterTrackerApp());

class WaterTrackerApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Water Tracker App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: WaterTrackerScreen(),
    );
  }
}

class WaterTrackerScreen extends StatefulWidget {
  @override
  _WaterTrackerScreenState createState() => _WaterTrackerScreenState();
}

class _WaterTrackerScreenState extends State<WaterTrackerScreen> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Water Tracker'),
      ),
      body: Center(
        child: Text('Water Consumption Tracker'),
      ),
    );
  }
}
```

This code sets up a basic Flutter app with a `WaterTrackerScreen` widget as the home screen. You can customize the UI inside the `WaterTrackerScreen` widget according to your app's requirements.

## Step 4: Implement Alarm Notifications

To implement alarm notifications, we will first create a helper class for handling notifications. Create a new file named `notification_helper.dart` in the `lib` directory and add the following code:

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';

class NotificationHelper {
  FlutterLocalNotificationsPlugin _flutterLocalNotificationsPlugin;

  NotificationHelper() {
    _flutterLocalNotificationsPlugin = FlutterLocalNotificationsPlugin();
    initializeNotifications();
  }

  Future<void> initializeNotifications() async {
    final initializationSettingsAndroid = AndroidInitializationSettings('app_icon');
    final initializationSettingsIOS = IOSInitializationSettings();
    final initializationSettings = InitializationSettings(
        initializationSettingsAndroid, initializationSettingsIOS);
    await _flutterLocalNotificationsPlugin.initialize(initializationSettings);
  }

  Future<void> scheduleNotification(
      {int id, String title, String body, DateTime scheduledTime}) async {
    final androidPlatformChannelSpecifics = AndroidNotificationDetails(
        'water_notification_channel', 'Water Reminder', 'Reminds you to drink water',
        importance: Importance.high, priority: Priority.high);
    final iOSPlatformChannelSpecifics = IOSNotificationDetails();
    final platformChannelSpecifics = NotificationDetails(
        androidPlatformChannelSpecifics, iOSPlatformChannelSpecifics);
    await _flutterLocalNotificationsPlugin.schedule(id, title, body,
        scheduledTime, platformChannelSpecifics);
  }
}
```

This helper class handles initializing and scheduling alarm notifications using the `flutter_local_notifications` package. Remember to replace `'app_icon'` with the actual name of your app's launcher icon.

## Step 5: Use Alarm Notifications in the App

Open the `lib/main.dart` file again and make the following changes:

1. Import the `notification_helper.dart` file:

```dart
import 'notification_helper.dart';
```

2. Add a `NotificationHelper` instance inside the `_WaterTrackerScreenState` class:

```dart
NotificationHelper _notificationHelper = NotificationHelper();
```

3. Use the `_notificationHelper` to schedule a notification. For example, you can add the following code inside the `build` method of the `_WaterTrackerScreenState` class:

```dart
_notificationHelper.scheduleNotification(
  id: 0,
  title: 'Drink Water!',
  body: 'It\'s time to have a glass of water.',
  scheduledTime: DateTime.now().add(Duration(minutes: 30)),
);
```

This code schedules a notification that reminds the user to drink water every 30 minutes.

## Step 6: Run the App

To run the app, use the following command in your terminal:

```shell
flutter run
```

Congratulations! You have successfully implemented a water consumption tracker app with alarm notifications using Flutter.

## Conclusion

In this tutorial, we learned how to create a basic water consumption tracker app and how to integrate alarm notifications using Flutter. Feel free to enhance the app by adding more features such as tracking daily water intake and setting personalized reminders. Happy coding!

`#Flutter` `#WaterTrackerApp`