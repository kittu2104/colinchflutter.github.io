---
layout: post
title: "Building a birthday reminder app with alarm functionality using Flutter"
description: " "
date: 2023-09-18
tags: [flutter, appdevelopment]
comments: true
share: true
---

In today's fast-paced world, it's easy to forget birthdays, which can lead to missed opportunities for celebration and connection. But worry not, because we can leverage the power of technology to create a handy birthday reminder app that will ensure you never miss an important date again. In this tutorial, we will be using Flutter, a popular cross-platform framework, to build our birthday reminder app with alarm functionality.

## Getting Started

To get started, make sure you have Flutter installed on your system. If not, you can refer to the official Flutter documentation for installation instructions.

## Setting up the Project

Open your preferred code editor and create a new Flutter project. You can use the following command in the terminal:

```bash
flutter create birthday_reminder_app
```

## Dependencies

To implement the alarm functionality, we need to add dependencies to our pubspec.yaml file. Open the file and add the following lines under the `dependencies` section:

```yaml
flutter_local_notifications: ^5.0.0
timezone: ^0.7.0
```

Save the file and run `flutter pub get` to fetch the added dependencies.

## Designing the User Interface

In the `lib` directory of your project, create a new file called `main.dart`. This will serve as the entry point for our app. Inside `main.dart`, let's start by defining the basic structure of our app's user interface. We can use Flutter's Material design widgets to achieve this.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(BirthdayReminderApp());
}

class BirthdayReminderApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Birthday Reminder',
      home: HomeScreen(),
    );
  }
}

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Birthday Reminder'),
      ),
      body: Center(
        child: Text(
          'Welcome to the Birthday Reminder App!',
          style: TextStyle(fontSize: 20),
        ),
      ),
    );
  }
}
```

## Adding Alarm Functionality

To add alarm functionality, we'll make use of the `flutter_local_notifications` package. Let's create a new file called `notification_service.dart` and define a class that will handle the notification-related logic.

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';

class NotificationService {
  FlutterLocalNotificationsPlugin _flutterLocalNotificationsPlugin =
      FlutterLocalNotificationsPlugin();

  initialize() {
    var initializationSettingsAndroid =
        AndroidInitializationSettings('@drawable/app_icon');
    var initializationSettingsIOS = IOSInitializationSettings();
    var initializationSettings = InitializationSettings(
        android: initializationSettingsAndroid, iOS: initializationSettingsIOS);

    _flutterLocalNotificationsPlugin.initialize(initializationSettings);
  }

  Future<void> scheduleNotification(DateTime date, String name) async {
    var androidPlatformChannelSpecifics = AndroidNotificationDetails(
      'channel_id', 'channel_name', 'channel_description',
      importance: Importance.high,
      priority: Priority.high,
    );
    var iOSPlatformChannelSpecifics = IOSNotificationDetails();
    var platformChannelSpecifics = NotificationDetails(
        android: androidPlatformChannelSpecifics,
        iOS: iOSPlatformChannelSpecifics);

    await _flutterLocalNotificationsPlugin.schedule(
        0, 'Birthday Reminder', 'It\'s $name\'s birthday!', date, platformChannelSpecifics);
  }
}
```

In the above code, `initialize()` method initializes the `flutter_local_notifications` plugin. The `scheduleNotification()` method schedules the notification with the provided date and name.

## Using the Notification Service

Now that we have our notification service ready, let's integrate it into our app. Update the `HomeScreen` class in `main.dart` as follows:

```dart
class HomeScreen extends StatelessWidget {
  final NotificationService _notificationService = NotificationService();

  @override
  Widget build(BuildContext context) {
    _notificationService.initialize();
    _notificationService.scheduleNotification(
        DateTime.now().add(Duration(seconds: 5)), 'John Doe');

    return Scaffold(
      appBar: AppBar(
        title: Text('Birthday Reminder'),
      ),
      body: Center(
        child: Text(
          'Welcome to the Birthday Reminder App!',
          style: TextStyle(fontSize: 20),
        ),
      ),
    );
  }
}
```

In this example, we initialize the `NotificationService` and schedule a test notification after 5 seconds for the fictitious person 'John Doe'. Remember to replace this test implementation with your actual logic for retrieving and scheduling the upcoming birthdays.

And that's it! You have successfully built a birthday reminder app with alarm functionality using Flutter. With this app, you can ensure that you never miss an important birthday again.

#flutter #appdevelopment