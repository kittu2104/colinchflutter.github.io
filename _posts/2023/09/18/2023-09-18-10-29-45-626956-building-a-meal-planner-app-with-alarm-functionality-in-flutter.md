---
layout: post
title: "Building a meal planner app with alarm functionality in Flutter"
description: " "
date: 2023-09-18
tags: [mealplanner]
comments: true
share: true
---

In this tutorial, we will walk you through the process of building a meal planner app with alarm functionality using Flutter, a cross-platform framework for building beautiful native apps. This app will allow users to plan their meals for the week and set reminders for meal times.

## Prerequisites

Before we begin, make sure you have the following installed:

- Flutter SDK
- Dart SDK
- Flutter IDE (e.g., Android Studio or Visual Studio Code) with the Flutter and Dart plugins installed

## Getting Started

To get started, open your preferred IDE and create a new Flutter project by running the following command:

```dart
$ flutter create meal_planner_app
```

Once the project is created, navigate to the `lib` directory and open the `main.dart` file. Replace the existing code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MealPlannerApp());
}

class MealPlannerApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Meal Planner',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Meal Planner'),
      ),
      body: Container(
        child: Center(
          child: Text(
            'Hello, Meal Planner!',
            style: TextStyle(fontSize: 20),
          ),
        ),
      ),
    );
  }
}
```

## Designing the Meal Planner UI

Next, let's design the UI for our meal planner app. Replace the `MyHomePage` class in `main.dart` with the following code:

```dart
class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Meal Planner'),
      ),
      body: Column(
        children: [
          Text(
            'Monday',
            style: TextStyle(
              fontSize: 24,
              fontWeight: FontWeight.bold,
            ),
          ),
          Expanded(
            child: ListView.builder(
              itemCount: 3,
              itemBuilder: (context, index) {
                return ListTile(
                  title: Text('Meal $index'),
                );
              },
            ),
          ),
        ],
      ),
    );
  }
}
```

In the code above, we have created a basic UI for the meal planner app with a ListView to display meals for each day of the week.

## Adding Alarm Functionality

To add alarm functionality, we can make use of the `flutter_local_notifications` package. Open the `pubspec.yaml` file and add the following dependency:

```yaml
dependencies:
  flutter_local_notifications: ^1.4.4
```

Next, run the following command to fetch the dependency:

```dart
$ flutter pub get
```

Once the dependency is added, replace the `MyHomePage` class in `main.dart` with the following code:

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';

class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin;

  @override
  void initState() {
    super.initState();
    initializeNotifications();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Meal Planner'),
      ),
      body: Column(
        children: [
          Text(
            'Monday',
            style: TextStyle(
              fontSize: 24,
              fontWeight: FontWeight.bold,
            ),
          ),
          Expanded(
            child: ListView.builder(
              itemCount: 3,
              itemBuilder: (context, index) {
                return ListTile(
                  title: Text('Meal $index'),
                  trailing: IconButton(
                    icon: Icon(Icons.alarm),
                    onPressed: () {
                      scheduleNotification();
                    },
                  ),
                );
              },
            ),
          ),
        ],
      ),
    );
  }

  void initializeNotifications() {
    flutterLocalNotificationsPlugin = FlutterLocalNotificationsPlugin();
    var initializationSettingsAndroid =
        AndroidInitializationSettings('app_icon');
    var initializationSettingsIOS = IOSInitializationSettings();
    var initializationSettings = InitializationSettings(
        android: initializationSettingsAndroid, iOS: initializationSettingsIOS);
    flutterLocalNotificationsPlugin.initialize(initializationSettings);
  }

  void scheduleNotification() async {
    var scheduledNotificationDateTime =
        DateTime.now().add(Duration(seconds: 5));
    var androidPlatformChannelSpecifics = AndroidNotificationDetails(
      'meal_planner_channel',
      'Meal Planner',
      'Channel for Meal Planner notifications',
    );
    var iOSPlatformChannelSpecifics = IOSNotificationDetails();
    var platformChannelSpecifics = NotificationDetails(
        android: androidPlatformChannelSpecifics,
        iOS: iOSPlatformChannelSpecifics);
    await flutterLocalNotificationsPlugin.schedule(
      0,
      'Meal Reminder',
      'It\'s time for your meal!',
      scheduledNotificationDateTime,
      platformChannelSpecifics,
      payload: 'meal_payload',
    );
  }
}
```

In the code above, we have imported the `flutter_local_notifications` package and added the necessary code for initializing notifications and scheduling notifications with a five-second delay when the alarm icon is pressed.

## Conclusion

In this tutorial, we have built a basic meal planner app with alarm functionality using Flutter. You can further enhance the app by allowing users to add their own meals, modify meal times, and implement more advanced alarm features. With Flutter's rich widgets and third-party packages, you can create powerful and feature-packed apps easily.

#flutter #mealplanner