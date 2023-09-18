---
layout: post
title: "How to implement a fitness tracker app with alarm notifications in Flutter"
description: " "
date: 2023-09-18
tags: []
comments: true
share: true
---

In this tutorial, we will learn how to build a fitness tracker app with alarm notifications using Flutter. Flutter is a popular open-source UI toolkit for building cross-platform apps.

## Prerequisites

Before we start, make sure you have the following prerequisites installed:

- [Flutter SDK](https://flutter.dev/docs/get-started/install)
- [Android Studio](https://developer.android.com/studio) (for Android development)
- [Xcode](https://developer.apple.com/xcode/) (for iOS development)
- A code editor of your choice (e.g., Visual Studio Code)

## Step 1: Create a New Flutter Project

To begin, open your terminal or command prompt and run the following command to create a new Flutter project:

```bash
flutter create fitness_tracker_app
```

## Step 2: Configure Alarm Notifications

To configure alarm notifications, we will use the `flutter_local_notifications` package. Add the package dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_local_notifications: ^5.0.0+2
```

Execute the following command to download the package:

```bash
flutter pub get
```

## Step 3: Design the User Interface

Design the user interface of your fitness tracker app. You can use Flutter's built-in widgets or customize with your own design. Here is an example of a basic UI structure:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(FitnessTrackerApp());
}

class FitnessTrackerApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Fitness Tracker',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: HomeScreen(),
    );
  }
}

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Fitness Tracker'),
      ),
      body: Center(
        child: Text(
          'Welcome to Fitness Tracker!',
          style: TextStyle(fontSize: 24),
        ),
      ),
    );
  }
}
```

## Step 4: Implement Alarm Notifications

To implement alarm notifications, create a new Dart file called `notification_service.dart`. Add the following code to the file:

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';

class NotificationService {
  final FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin =
      FlutterLocalNotificationsPlugin();

  Future<void> initialize() async {
    final initializationSettingsAndroid =
        AndroidInitializationSettings('app_icon');
    final initializationSettingsIOS = IOSInitializationSettings();
    final initializationSettings = InitializationSettings(
        android: initializationSettingsAndroid, iOS: initializationSettingsIOS);

    await flutterLocalNotificationsPlugin.initialize(initializationSettings);
  }

  Future<void> scheduleNotification(DateTime notificationTime) async {
    final androidPlatformChannelSpecifics = AndroidNotificationDetails(
        'channel_id', 'channel_name', 'channel_description',
        importance: Importance.max, priority: Priority.high);
    final iOSPlatformChannelSpecifics = IOSNotificationDetails();
    final platformChannelSpecifics = NotificationDetails(
        android: androidPlatformChannelSpecifics,
        iOS: iOSPlatformChannelSpecifics);

    await flutterLocalNotificationsPlugin.schedule(
        0,
        'Fitness Tracker',
        'Time to exercise',
        notificationTime,
        platformChannelSpecifics);
  }
}
```

## Step 5: Trigger Alarm Notifications

To trigger alarm notifications, modify the `HomeScreen` widget in your `main.dart` file as follows:

```dart
class HomeScreen extends StatelessWidget {
  final notificationService = NotificationService();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Fitness Tracker'),
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: () async {
            await notificationService.initialize();

            // Schedule notification after 5 seconds
            final notificationTime = DateTime.now().add(Duration(seconds: 5));
            await notificationService.scheduleNotification(notificationTime);
          },
          child: Text('Set Alarm'),
        ),
      ),
    );
  }
}
```

## Step 6: Test and Run the App

Now, you can test and run your fitness tracker app with alarm notifications. Connect your device (Android or iOS) or start an emulator, then execute the following command to launch the app:

```bash
flutter run
```

## Conclusion

Congratulations! You have successfully implemented a fitness tracker app with alarm notifications in Flutter. Now you can further enhance the app by adding more features such as tracking exercise data and setting personalized goals.