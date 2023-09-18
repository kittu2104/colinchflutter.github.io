---
layout: post
title: "Implementing a task planner app with priority-based alarms using Flutter Alarm Manager"
description: " "
date: 2023-09-18
tags: [Flutter, TaskPlanner]
comments: true
share: true
---

As our lives become busier and more hectic, it's important to stay organized and manage our tasks effectively. One way to achieve this is by using a task planner app that not only keeps track of our to-do list but also provides priority-based alarms to ensure timely completion of important tasks. In this blog post, we will explore how to implement such a task planner app using Flutter Alarm Manager.

## What is Flutter Alarm Manager?

Flutter Alarm Manager is a plugin for Flutter apps that allows you to schedule and handle alarms. It offers a simple and easy-to-use interface for managing alarms and callbacks, making it ideal for developing task planner apps.

## Setting Up the Project

To get started, make sure you have the Flutter SDK installed on your machine. Create a new Flutter project using the following command:

```shell
flutter create task_planner
```

Next, add the Flutter Alarm Manager plugin to your dependencies in the `pubspec.yaml` file:

```yaml
dependencies:
  flutter_alarm_manager: ^1.0.0
```

Run the following command to fetch the dependencies:

```shell
flutter pub get
```

## Designing the Task Planner UI

Before we dive into the implementation details, let's design the UI for our task planner app. We'll create a simple interface that allows users to add new tasks with priority and set alarms corresponding to each task.

The UI can consist of a list view to display tasks, a form to add new tasks, and a dialog picker to set alarms.

## Implementing the Task Planner Logic

Now, let's implement the logic behind the task planner app. We'll start by creating a model class for tasks:

```dart
class Task {
  String title;
  int priority;
  DateTime alarmTime;

  Task({required this.title, required this.priority, required this.alarmTime});
}
```

Next, we'll create a stateful widget to handle the task planner functionality:

```dart
class TaskPlannerApp extends StatefulWidget {
  @override
  _TaskPlannerAppState createState() => _TaskPlannerAppState();
}

class _TaskPlannerAppState extends State<TaskPlannerApp> {
  List<Task> tasks = [];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Task Planner'),
      ),
      body: ListView.builder(
        itemCount: tasks.length,
        itemBuilder: (context, index) {
          return ListTile(
            title: Text(tasks[index].title),
            subtitle: Text(tasks[index].priority.toString()),
            trailing: IconButton(
              icon: Icon(Icons.delete),
              onPressed: () {
                setState(() {
                  tasks.removeAt(index);
                });
              },
            ),
          );
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          _addTaskDialog(context);
        },
        child: Icon(Icons.add),
      ),
    );
  }

  Future<void> _addTaskDialog(BuildContext context) async {
    // Show dialog to add new task
  }
}
```

In the `_addTaskDialog` method, we can add a dialog that prompts the user to enter the task details, including the priority and alarm time. We'll use the Flutter Alarm Manager plugin to schedule alarms based on the selected time.

## Scheduling Alarms using Flutter Alarm Manager

To schedule alarms, we need to use the `flutter_alarm_manager` plugin. We can add it to our `_addTaskDialog` method as follows:

```dart
import 'package:flutter_alarm_manager/flutter_alarm_manager.dart';

...

Future<void> _addTaskDialog(BuildContext context) async {
  DateTime? alarmTime;

  await showDialog(
    context: context,
    builder: (context) {
      return AlertDialog(
        title: Text('Add New Task'),
        content: Column(
          // Add form fields for task details
        ),
        actions: [
          TextButton(
            onPressed: () => Navigator.pop(context),
            child: Text('Cancel'),
          ),
          ElevatedButton(
            onPressed: () {
              // Validate and save task details

              // Schedule alarm
              FlutterAlarmManager.oneShotAt(alarmTime!, alarmId, callback);
              
              Navigator.pop(context);
            },
            child: Text('Add Task'),
          ),
        ],
      );
    },
  );
}
```

Here, we schedule a one-shot alarm using the `FlutterAlarmManager.oneShotAt` method by passing the selected `alarmTime`, a unique `alarmId`, and a `callback` function to handle the alarm event.

## Conclusion

In this blog post, we learned how to implement a task planner app with priority-based alarms using the Flutter Alarm Manager plugin. We designed the UI to add tasks and scheduled alarms based on user input. This enables users to stay organized and complete their tasks more efficiently. By incorporating this functionality into your own Flutter app, you can help users manage their tasks and goals effectively.

#Flutter #TaskPlanner #AlarmManager