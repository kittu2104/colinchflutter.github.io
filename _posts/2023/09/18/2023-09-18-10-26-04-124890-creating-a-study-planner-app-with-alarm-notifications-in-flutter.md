---
layout: post
title: "Creating a study planner app with alarm notifications in Flutter"
description: " "
date: 2023-09-18
tags: [StudyPlannerApp]
comments: true
share: true
---

## Introduction
In today's fast-paced world, staying organized and managing time effectively is crucial, especially for students. With the help of technology, we can create a study planner app that not only assists students in organizing their study sessions but also notifies them with alarm reminders. In this tutorial, we will use Flutter, a popular cross-platform framework, to build a study planner app with alarm notifications.

## Prerequisites
Before we dive into the implementation, make sure you have the following prerequisites:
- Flutter SDK installed on your machine
- A basic understanding of Flutter and Dart programming language

## Step 1: Setup
First, create a new Flutter project using the following command in your terminal:
```shell
flutter create study_planner_app
```

## Step 2: Designing the User Interface
Next, we will design the user interface for our study planner app. Start by modifying the 'lib/main.dart' file as follows:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(StudyPlannerApp());
}

class StudyPlannerApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Study Planner',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: StudyPlannerScreen(),
    );
  }
}

class StudyPlannerScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Study Planner'),
      ),
      body: Center(
        child: Text('Study Planner Screen'),
      ),
    );
  }
}

```

## Step 3: Adding Alarm Notifications
To incorporate alarm notifications into our study planner app, we will use the `flutter_local_notifications` package. Add the following dependency to your pubspec.yaml file:

```yaml
dependencies:
  flutter_local_notifications: ^6.0.0
```

Then, import the required packages and modify the code as shown below:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_local_notifications/flutter_local_notifications.dart';

final FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin =
    FlutterLocalNotificationsPlugin();

void main() async {
  WidgetsFlutterBinding.ensureInitialized();

  // Configuration for initializing the notifications plugin
  final AndroidInitializationSettings initializationSettingsAndroid =
      AndroidInitializationSettings('app_icon');
  final InitializationSettings initializationSettings = InitializationSettings(
    android: initializationSettingsAndroid,
  );
  await flutterLocalNotificationsPlugin.initialize(initializationSettings);

  runApp(StudyPlannerApp());
}

// ... Continue with the remaining code

```

## Step 4: Adding Study Task and Alarm
Now, let's add the functionality to create study tasks and set alarms for them. Modify the `StudyPlannerScreen` as follows:

```dart
// ... Previous code

class StudyPlannerScreen extends StatefulWidget {
  @override
  _StudyPlannerScreenState createState() => _StudyPlannerScreenState();
}

class _StudyPlannerScreenState extends State<StudyPlannerScreen> {
  List<String> tasks = [];

  Future<void> _addStudyTask() async {
    final String task = await showDialog<String>(
      context: context,
      builder: (BuildContext context) {
        String taskText = '';
        return AlertDialog(
          title: const Text('Add Study Task'),
          content: TextField(
            onChanged: (String value) {
              taskText = value;
            },
          ),
          actions: <Widget>[
            TextButton(
              onPressed: () {
                Navigator.of(context).pop(taskText.trim());
              },
              child: const Text('Add'),
            ),
          ],
        );
      },
    );

    if (task != null) {
      setState(() {
        tasks.add(task);
      });
      _scheduleAlarm(task);
    }
  }

  Future<void> _scheduleAlarm(String task) async {
    // Configure the notification details
    const AndroidNotificationDetails androidPlatformChannelSpecifics =
        AndroidNotificationDetails(
      'study_planner_app',
      'Study Planner',
      'Notification for Study Planner',
      importance: Importance.max,
      priority: Priority.high,
      showWhen: false,
    );
    const NotificationDetails platformChannelSpecifics =
        NotificationDetails(android: androidPlatformChannelSpecifics);

    // Schedule the alarm after 10 seconds
    await flutterLocalNotificationsPlugin.periodicallyShow(
      Random().nextInt(100),
      'Study Planner',
      'Time to study: $task',
      RepeatInterval.everyMinute,
      platformChannelSpecifics,
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Study Planner'),
      ),
      body: Column(
        children: [
          ElevatedButton(
            onPressed: _addStudyTask,
            child: Text('Add Study Task'),
          ),
          Expanded(
            child: ListView.builder(
              itemCount: tasks.length,
              itemBuilder: (BuildContext context, int index) {
                return ListTile(
                  title: Text(tasks[index]),
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

## Conclusion
In this tutorial, we have covered how to create a study planner app with alarm notifications using Flutter. By following these steps, you can help students stay organized and manage their study sessions effectively. Remember to run the app on your preferred device or emulator to see it in action. Happy coding!

## Hashtags
#Flutter #StudyPlannerApp