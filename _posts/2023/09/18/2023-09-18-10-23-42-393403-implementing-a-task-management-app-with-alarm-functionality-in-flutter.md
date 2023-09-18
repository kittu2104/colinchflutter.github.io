---
layout: post
title: "Implementing a task management app with alarm functionality in Flutter"
description: " "
date: 2023-09-18
tags: [taskmanagement]
comments: true
share: true
---

Flutter is an open-source framework developed by Google for building cross-platform applications. In this tutorial, we will walk through the steps of implementing a task management app with alarm functionality using Flutter.

## Prerequisites

Before we get started, make sure you have the following prerequisites installed on your machine:

- [Flutter SDK](https://flutter.dev/docs/get-started/install)
- [Dart SDK](https://dart.dev/get-dart)

## Creating a Flutter Project

To create a new Flutter project, run the following command in your terminal:

```bash
flutter create task_manager
```

This will create a new directory named `task_manager` with the necessary project files.

## Designing the User Interface

For this app, we will use a simple UI consisting of a list of tasks that users can add, complete, and set alarms for. 

### Task List Screen

Start by modifying the `lib/main.dart` file to create a `TaskListScreen` widget that displays the list of tasks:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(TaskManagerApp());
}

class TaskManagerApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Task Manager'),
        ),
        body: TaskListScreen(),
      ),
    );
  }
}

class TaskListScreen extends StatefulWidget {
  @override
  _TaskListScreenState createState() => _TaskListScreenState();
}

class _TaskListScreenState extends State<TaskListScreen> {
  List<String> tasks = [];

  @override
  Widget build(BuildContext context) {
    return ListView.builder(
      itemCount: tasks.length,
      itemBuilder: (context, index) {
        final task = tasks[index];
        return ListTile(
          title: Text(task),
        );
      },
    );
  }
}
```

### Adding Task Form

To add tasks, we need to create a form where users can input task details. Modify the `TaskListScreen` widget to include a floating action button that opens the task form:

```dart
class _TaskListScreenState extends State<TaskListScreen> {
  // ...

  void _openTaskForm() {
    showDialog(
      context: context,
      builder: (context) => AlertDialog(
        title: Text('Add Task'),
        content: Column(
          mainAxisSize: MainAxisSize.min,
          children: [
            TextField(
              decoration: InputDecoration(
                labelText: 'Task Name',
              ),
            ),
            SizedBox(height: 16),
            ElevatedButton(
              onPressed: () {
                // Save the task and close the dialog
                Navigator.of(context).pop();
              },
              child: Text('Add Task'),
            ),
          ],
        ),
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      // ...

      floatingActionButton: FloatingActionButton(
        onPressed: _openTaskForm,
        child: Icon(Icons.add),
      ),
    );
  }
}
```

## Implementing Alarm Functionality

To add alarm functionality to our app, we can use the `flutter_local_notifications` package. Add it as a dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_local_notifications: ^flutter_local_notifications_version
```

Replace `flutter_local_notifications_version` with the latest version of the package.

Next, import the necessary packages in the `lib/main.dart` file:

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';

final FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin =
    FlutterLocalNotificationsPlugin();
```

Initialize the notification plugin in the `main()` function:

```dart
void main() async {
  WidgetsFlutterBinding.ensureInitialized();

  final initializationSettingsAndroid =
      AndroidInitializationSettings('app_icon');
  final initializationSettingsIOS = IOSInitializationSettings();
  final initializationSettings = InitializationSettings(
    android: initializationSettingsAndroid,
    iOS: initializationSettingsIOS,
  );

  await flutterLocalNotificationsPlugin.initialize(initializationSettings);

  runApp(TaskManagerApp());
}
```

Now, we can trigger a notification when a task is added. Modify the `_openTaskForm()` method in the `TaskListScreen` widget:

```dart
void _openTaskForm() {
  showDialog(
    context: context,
    builder: (context) => AlertDialog(
      title: Text('Add Task'),
      content: Column(
        mainAxisSize: MainAxisSize.min,
        children: [
          TextField(
            decoration: InputDecoration(
              labelText: 'Task Name',
            ),
          ),
          SizedBox(height: 16),
          ElevatedButton(
            onPressed: () async {
              // Save the task and close the dialog
              final taskName = _taskNameController.text;
              tasks.add(taskName);
              Navigator.of(context).pop();

              // Show a notification
              const androidPlatformChannelSpecifics = AndroidNotificationDetails(
                'task_channel',
                'Task Notifications',
                'Notifications for added tasks',
                importance: Importance.max,
                priority: Priority.high,
              );
              const iOSPlatformChannelSpecifics = IOSNotificationDetails();
              const platformChannelSpecifics = NotificationDetails(
                android: androidPlatformChannelSpecifics,
                iOS: iOSPlatformChannelSpecifics,
              );

              await flutterLocalNotificationsPlugin.show(
                0,
                'New Task Added',
                taskName,
                platformChannelSpecifics,
              );
            },
            child: Text('Add Task'),
          ),
        ],
      ),
    ),
  );
}
```

## Conclusion

In this tutorial, we have learned how to implement a task management app with alarm functionality in Flutter. We designed a simple UI to display tasks and added the ability to add tasks with notifications using the `flutter_local_notifications` package. With this foundation, you can further enhance the app by adding features like task completion and task editing.

#flutter #taskmanagement #alarmfunctionality