---
layout: post
title: "Implementing a reminder app with location-based alarms using Flutter Alarm Manager"
description: " "
date: 2023-09-18
tags: [Flutter, FlutterAlarmManager]
comments: true
share: true
---

In today's fast-paced world, staying organized is crucial. A reminder app can be a handy tool for keeping track of important tasks and events. With Flutter Alarm Manager, we can take it a step further and add location-based alarms to ensure we never miss anything based on our geographical location. In this blog post, we will explore how to implement a reminder app with location-based alarms using Flutter Alarm Manager.

## What is Flutter Alarm Manager?

Flutter Alarm Manager is a plugin that allows us to schedule and manage alarms in Flutter applications. It provides a simple interface to schedule alarms at specific times or intervals. The plugin also supports the ability to set alarms based on the user's location, making it ideal for implementing location-based reminders in our app.

## Prerequisites

To follow along, make sure you have the following:

- Flutter SDK installed on your machine
- A compatible code editor (e.g., Visual Studio Code)
- Basic knowledge of Flutter and Dart programming language

## Setting Up the Project

Let's start by creating a new Flutter project. Open your preferred command-line interface and run the following command:

```bash
flutter create reminder_app
```

This will create a new Flutter project called "reminder_app". Navigate into the project directory:

```bash
cd reminder_app
```

Next, open the project in your code editor.

## Adding Dependencies

We need to add the Flutter Alarm Manager plugin to our project. Open the `pubspec.yaml` file and add the following lines in the `dependencies` section:

```yaml
dependencies:
  flutter_alarm_manager: ^0.4.1
```

Save the file and run the command `flutter pub get` in your terminal to fetch the dependencies.

## Implementing the Reminder App

Now that our project is set up with the necessary dependencies, we can start implementing the reminder app. Let's create a new Dart file called `main.dart`.

Start by importing the required dependencies:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_alarm_manager/flutter_alarm_manager.dart';
```

Next, create a new Flutter widget, which will serve as the main app screen:

```dart
class ReminderApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Reminder App',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Reminder App'),
        ),
        body: Center(
          child: Text('Welcome to Reminder App'),
        ),
      ),
    );
  }
}
```

In the `build` method of the `ReminderApp` widget, we have a simple layout with a centered text widget displaying a welcome message.

Now, let's add the necessary code to schedule a location-based alarm. Add the following code inside the `ReminderApp` class:

```dart
void _scheduleLocationAlarm() {
  final locationAlarm = Alarm(
    id: 1,
    title: 'Grocery Shopping',
    location: 'Supermarket',
    longitude: 12.345,
    latitude: 67.890,
  );

  FlutterAlarmManager.schedule(
    locationAlarm,
    Duration(minutes: 30),
    showNotification: true,
  );
}
```

The `_scheduleLocationAlarm` method creates an instance of the `Alarm` class with the desired properties, such as `id`, `title`, `location`, `longitude`, and `latitude`. It then uses the `FlutterAlarmManager.schedule` method to schedule the alarm to trigger in 30 minutes from the current time.

To initialize the app and schedule the alarm, add the following code inside the `main` function:

```dart
void main() {
  runApp(ReminderApp());
  _scheduleLocationAlarm();
}
```

Here, we call the `_scheduleLocationAlarm` method after initializing the app using the `runApp` function.

## Testing the App

To test the app, we need to run it on a physical device or emulator that supports location services. Run the following command in your terminal:

```bash
flutter run
```

The app will start, and after 30 minutes, a notification will be displayed, reminding you to go grocery shopping at the specified location.

## Conclusion

In this blog post, we learned how to implement a reminder app with location-based alarms using Flutter Alarm Manager. By leveraging the Flutter Alarm Manager plugin, we were able to schedule alarms based on the user's location, ensuring timely reminders and improved organization. With further exploration, we can enhance our app with additional features such as recurring alarms and custom notification styles. Happy coding!

## #Flutter #FlutterAlarmManager