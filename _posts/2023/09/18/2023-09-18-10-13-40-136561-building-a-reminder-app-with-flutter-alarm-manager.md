---
layout: post
title: "Building a reminder app with Flutter Alarm Manager"
description: " "
date: 2023-09-18
tags: [reminderapp]
comments: true
share: true
---

In this blog post, we will explore how to build a reminder app using the Flutter framework and the Flutter Alarm Manager package. This app will allow users to set reminders for important tasks, events, or appointments and receive notifications at the specified time.

## Prerequisites
To follow along with this tutorial, you should have a basic understanding of Flutter and have Flutter SDK installed on your machine.

## Getting Started
First, let's create a new Flutter project by running the following command in your terminal:
```bash
flutter create reminder_app
```

Next, navigate to the project directory:
```bash
cd reminder_app
``` 

## Adding Packages
To utilize the Flutter Alarm Manager package, we need to add it to our `pubspec.yaml` file. Open the file and add the following lines under the `dependencies` section:

```yaml
dependencies:
  flutter_alarm_manager: ^0.4.2
```

Save the file and run the following command to fetch the packages:
```bash
flutter pub get
```

## Setting Up Alarm Manager
Now, let's set up the Alarm Manager in our Flutter app. Open the `main.dart` file and add the following imports at the top:

```dart
import 'package:flutter_alarm_manager/flutter_alarm_manager.dart';
import 'package:flutter_ringtone_player/flutter_ringtone_player.dart';
```

Next, replace the existing code in the `main` function with the following code:

```dart
void main() async {
  WidgetsFlutterBinding.ensureInitialized();

  // Registering the alarm callback
  FlutterAlarmManager.initialize();

  // Callback function when alarm triggers
  FlutterAlarmManager.addAlarmCallback(alarmCallback);

  runApp(MyApp());
}
```

## Implementing the Reminder Screen
Create a new file named `reminder_screen.dart` in the `lib` directory. This file will contain the UI for setting reminders. 

```dart
import 'package:flutter/material.dart';

class ReminderScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Reminder App'),
      ),
      body: Center(
        child: Text('Reminder Screen'),
      ),
    );
  }
}
```

## Setting up Notifications
Create a new file named `reminder_manager.dart` in the `lib` directory. This file will contain the logic for handling reminder notifications.

```dart
import 'package:flutter_alarm_manager/flutter_alarm_manager.dart';
import 'package:flutter_ringtone_player/flutter_ringtone_player.dart';

void alarmCallback() {
  FlutterRingtonePlayer.playRingtone();
  // Add logic for showing reminder notification
}
```

## Wiring it all together
Open the `main.dart` file again and replace the existing code with the following code:

```dart
import 'package:flutter/material.dart';

import 'reminder_screen.dart';
import 'reminder_manager.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();

  FlutterAlarmManager.initialize();
  FlutterAlarmManager.addAlarmCallback(alarmCallback);

  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Reminder App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: ReminderScreen(),
    );
  }
}
```

## Conclusion
With the Flutter Alarm Manager package, building a reminder app in Flutter becomes a breeze. You can now enhance the app by adding more features like date and time selection, persistence of reminders, etc.

Feel free to explore the Flutter Alarm Manager package documentation for more functionality and customization options.

#flutter #reminderapp #flutteralarmmanager