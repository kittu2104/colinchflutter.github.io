---
layout: post
title: "Creating an event planner app using Flutter Alarm Manager"
description: " "
date: 2023-09-18
tags: [Building, #Setting]
comments: true
share: true
---

In today's fast-paced world, keeping track of important events and appointments can be a challenging task. However, with the power of technology, we can create an event planner app to help us stay organized and never miss an important event. In this tutorial, we will explore how to build an event planner app using Flutter and implement an alarm manager to notify users of upcoming events.

##Setting Up the Project

To get started, make sure you have Flutter and Dart installed on your machine. Once you have Flutter installed, open your chosen IDE and create a new Flutter application.

##Creating the UI

The first step in building our event planner app is to create the user interface (UI). Using Flutter's widget-based approach, we can create a visually appealing and intuitive UI.

We can start by creating a simple home page that displays a list of upcoming events. Each event item will contain the event's name, date, and time. We can use the Flutter ListView widget to display the list of events.

```dart
import 'package:flutter/material.dart';

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Event Planner'),
      ),
      body: ListView.builder(
        itemCount: events.length,
        itemBuilder: (context, index) {
          return ListTile(
            title: Text(events[index].name),
            subtitle: Text(events[index].dateTime.toString()),
          );
        },
      ),
    );
  }
}

class Event {
  final String name;
  final DateTime dateTime;

  Event({required this.name, required this.dateTime});
}

List<Event> events = [
  Event(name: 'Meeting', dateTime: DateTime.now().add(Duration(days: 1))),
  Event(name: 'Birthday Party', dateTime: DateTime.now().add(Duration(days: 3))),
  Event(name: 'Conference', dateTime: DateTime.now().add(Duration(days: 5))),
];
```

##Implementing the Alarm Manager

To notify users of upcoming events, we will implement an alarm manager that triggers an alarm at the specified event's date and time. We can use the flutter_local_notifications package to handle notifications in Flutter.

First, add the `flutter_local_notifications` dependency to your `pubspec.yaml` file and run `flutter pub get` to download the package.

Next, we can create a `NotificationService` class to handle the initialization and scheduling of notifications.

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';

class NotificationService {
  final FlutterLocalNotificationsPlugin notificationsPlugin =
      FlutterLocalNotificationsPlugin();

  Future initialize() async {
    final InitializationSettings initializationSettings =
        InitializationSettings(
      android: AndroidInitializationSettings('app_icon'),
    );
    await notificationsPlugin.initialize(initializationSettings);
  }

  Future scheduleNotification(String title, DateTime dateTime) async {
    final AndroidNotificationDetails androidDetails = AndroidNotificationDetails(
      'channel_id',
      'channel_name',
      'channel_description',
    );
    final NotificationDetails platformDetails =
        NotificationDetails(android: androidDetails);

    await notificationsPlugin.schedule(
      0,
      title,
      'Upcoming event!',
      dateTime,
      platformDetails,
    );
  }
}
```

Finally, we can integrate the `NotificationService` into our app by initializing it and scheduling notifications in the event planner app.

```dart
void main() async {
  WidgetsFlutterBinding.ensureInitialized();

  final notificationService = NotificationService();
  await notificationService.initialize();

  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Event Planner',
      home: HomePage(),
    );
  }
}
```

##Conclusion

In this tutorial, we discussed how to create an event planner app using Flutter and implement an alarm manager to notify users of upcoming events. By leveraging Flutter's powerful widget-based UI, along with the `flutter_local_notifications` package, we were able to build a functional and user-friendly event planner app. With this knowledge, you can now explore further enhancements, such as adding event creation functionality and integrating with a backend to store events. #Flutter #EventPlanner #AlarmManager