---
layout: post
title: "How to implement a workout tracker app with alarm notifications in Flutter"
description: " "
date: 2023-09-18
tags: [WorkoutTracker]
comments: true
share: true
---

In today's fast-paced world, keeping track of your workouts and staying consistent with your fitness goals can be challenging. Fortunately, Flutter, a cross-platform framework developed by Google, allows us to build beautiful and versatile mobile applications quickly. In this tutorial, we will guide you through the process of building a workout tracker app with alarm notifications in Flutter.

## Prerequisites

Before getting started, make sure you have the following:

- Flutter SDK installed on your machine
- A code editor of your choice (e.g., Visual Studio Code, Android Studio)
- Basic knowledge of Flutter and Dart programming language

## Setting up the Project

1. Open your preferred command line interface and navigate to the directory where you want to create your project.

2. Run the following command to create a new Flutter project:
```bash
flutter create workout_tracker_app
```

3. Navigate to the project directory:
```bash
cd workout_tracker_app
```

## Designing the User Interface

1. Open the `lib/main.dart` file in your code editor.

2. Remove the existing boilerplate code and replace it with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(WorkoutTrackerApp());
}

class WorkoutTrackerApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Workout Tracker',
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
        title: Text('Workout Tracker'),
      ),
      body: Center(
        child: Text('Welcome to Workout Tracker'),
      ),
    );
  }
}
```

This code sets up a basic Flutter application with a home page containing an app bar and a centered text widget.

3. Save the file and run the app using the following command:
```bash
flutter run
```
You should now see the app running on your connected device or emulator.

## Adding Alarm Notifications

1. To include alarm notification functionality in our app, we need to add the `flutter_local_notifications` package as a dependency. Open the `pubspec.yaml` file and add the following line under the `dependencies` section:

```yaml
dependencies:
  flutter_local_notifications: ^8.2.0
```

2. Run the following command to fetch the package:
```bash
flutter pub get
```

3. Open the `lib/main.dart` file and import the `flutter_local_notifications` package:

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';
```

4. Add the following code inside the `HomePage` class, just before the `build` method:

```dart
FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin =
    FlutterLocalNotificationsPlugin();
```

5. To initialize the notification plugin, add the following code inside the `main` method:

```dart
void main() async {
  WidgetsFlutterBinding.ensureInitialized();

  const AndroidInitializationSettings initializationSettingsAndroid =
      AndroidInitializationSettings('app_icon');

  final InitializationSettings initializationSettings =
      InitializationSettings(
    android: initializationSettingsAndroid,
  );

  await flutterLocalNotificationsPlugin.initialize(
    initializationSettings,
  );

  runApp(WorkoutTrackerApp());
}
```

Make sure you replace `'app_icon'` with the name of your app icon image file.

6. Now, to display a notification, add the following code inside the `build` method of the `HomePage` class:

```dart
void _showNotification() async {
  const AndroidNotificationDetails androidPlatformChannelSpecifics =
      AndroidNotificationDetails(
    'workout_tracker_app_id',
    'Workout Tracker App',
    'Notifies user about workout sessions',
    importance: Importance.high,
    priority: Priority.defaultPriority,
    playSound: true,
    enableLights: true,
    enableVibration: true,
    ledColor: Colors.blue,
    ledOnMs: 1000,
    ledOffMs: 500,
    sound: RawResourceAndroidNotificationSound('notification_sound'),
  );

  const NotificationDetails platformChannelSpecifics =
      NotificationDetails(android: androidPlatformChannelSpecifics);

  await flutterLocalNotificationsPlugin.show(
    0,
    'Workout Reminder',
    'It\'s time to start your workout!',
    platformChannelSpecifics,
  );
}
```

Ensure that you have a sound file named `'notification_sound.wav'` or replace it with the name of your custom sound.

7. Update the `body` of the `HomePage` class with the following code:

```dart
body: Center(
  child: ElevatedButton(
   child: Text('Set Workout Reminder'),
   onPressed: _showNotification,
  ),
),
```

This code adds a button that triggers the `_showNotification` method when pressed.

8. Save the file and hot-reload the app by saving the changes and typing `r` in your command line interface.

Congratulations! You now have a workout tracker app with alarm notifications in Flutter. Feel free to customize the design and add more features to enhance the user experience.

*#Flutter #WorkoutTracker*