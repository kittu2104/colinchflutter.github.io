---
layout: post
title: "Building a task tracking app with alarm functionality using Flutter"
description: " "
date: 2023-09-18
tags: [tasktracker]
comments: true
share: true
---

In today's fast-paced world, staying organized and managing our tasks efficiently has become increasingly important. With the help of mobile apps, we can easily keep track of our tasks and set reminders to ensure we stay on top of our schedules. In this blog post, we will explore how to build a task tracking app with alarm functionality using Flutter.

## What is Flutter?

[Flutter](https://flutter.dev/) is an open-source UI software development kit created by Google. It allows developers to build beautiful and fast native applications for mobile, web, and desktop using a single codebase. Flutter uses the Dart programming language and enables hot-reloading, making it a popular choice for building cross-platform mobile apps.

## Setting up the Flutter Project

Before we begin building our task tracking app, we need to set up a Flutter project. Assuming you have Flutter installed, open your terminal or command prompt and run the following command:

```shell
flutter create task_tracker
```

This command creates a new Flutter project named "task_tracker." Once the project is created, navigate to the project directory using `cd task_tracker`. 

Next, open the project in your preferred code editor.

## Designing the User Interface

The first step in building our task tracking app is designing the user interface. Flutter provides a wide range of widgets that help us create flexible and responsive UIs.

For our task tracking app, we will create a simple interface consisting of a list of tasks and a button to add new tasks. Each task will have a title, description, and alarm time.

Let's start by creating a new file named "home_screen.dart" in the "lib" directory of our project. In this file, we will define our home screen widget.

```dart
import 'package:flutter/material.dart';

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Task Tracker'),
      ),
      body: ListView.builder(
        itemCount: tasks.length,
        itemBuilder: (context, index) {
          // build task item widget
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          // navigate to add task screen
        },
        child: Icon(Icons.add),
      ),
    );
  }
}
```

In the above code snippet, we define the `HomeScreen` class as a `StatelessWidget`. It includes an `AppBar` with the title "Task Tracker" and a `ListView.builder` widget to display the list of tasks.

Inside the `ListView.builder` widget, we will generate a widget for each task using the `itemBuilder` callback. We will define the task item widget separately.

## Implementing Alarm Functionality

To implement the alarm functionality, we will utilize the Flutter Local Notifications package. This package allows us to schedule and display notifications on the device.

First, let's add the Flutter Local Notifications package to our `pubspec.yaml` file:

```yaml
dependencies:
  flutter_local_notifications: ^5.0.0
```

After saving the changes, run `flutter pub get` in the terminal to fetch the package.

Now, we can create a new file named "notification_service.dart" in the "lib" directory. This file will contain the necessary code to initialize the notification service and schedule notifications.

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';

class NotificationService {
  FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin;

  Future initialize() async {
    flutterLocalNotificationsPlugin = FlutterLocalNotificationsPlugin();
    const initializationSettingsAndroid = AndroidInitializationSettings('app_icon');
    final initializationSettings = InitializationSettings(android: initializationSettingsAndroid);
    await flutterLocalNotificationsPlugin.initialize(initializationSettings);
  }

  Future scheduleNotification(String title, String description, DateTime dateTime) async {
    final androidPlatformChannelSpecifics = AndroidNotificationDetails(
        'channel_id', 'channel_name', 'channel_description',
        importance: Importance.high, priority: Priority.high);
    
    final notificationDetails = NotificationDetails(android: androidPlatformChannelSpecifics);

    await flutterLocalNotificationsPlugin.schedule(
        0, title, description, dateTime, notificationDetails);
  }
}
```

In the `initialize` method, we initialize the `flutterLocalNotificationsPlugin` and configure the Android platform settings. We then schedule a notification using the `scheduleNotification` method, which takes the title, description, and date-time as parameters.

## Adding Task Creation and Alarm Setting

To add the task creation functionality, we will create a new file named "add_task_screen.dart" in the "lib" directory. In this file, we will define a form to collect the task details from the user.

Inside the `AddTaskScreen` class, we will display input fields for the task title, description, and alarm time. We will also include a button to save the task and schedule the alarm.

Once the user saves the task, we will navigate back to the home screen and display the newly added task in the task list.

## Conclusion

In this blog post, we explored how to build a task tracking app with alarm functionality using Flutter. We started by setting up a Flutter project, designing the user interface, and implementing the alarm functionality using Flutter Local Notifications package. Finally, we added task creation and alarm setting features to our app.

With Flutter's powerful and flexible abilities, you can create highly functional and visually appealing task tracking apps that will help users stay organized and manage their tasks effectively.

#flutter #tasktracker