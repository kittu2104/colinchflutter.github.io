---
layout: post
title: "Implementing data synchronization across devices in a StatelessWidget in Flutter"
description: " "
date: 2023-09-24
tags: [flutter, dataSync]
comments: true
share: true
---

## Setting Up Firebase Realtime Database

To achieve data synchronization, we will leverage Firebase Realtime Database. Follow these steps to set it up in your Flutter project:

1. Create a new Firebase project in the Firebase Console.
2. Connect your Flutter app to the project by adding the necessary dependencies and configuration files.
3. Enable Firebase Realtime Database in the Firebase Console.

## Designing the Data Model

Before we begin implementing data synchronization, it's crucial to define the data model that will be synchronized across devices. Let's take a simple to-do list app as an example. The data model could consist of a `Task` class with properties like `id`, `title`, `description`, and `completed`.

```dart
class Task {
  final String id;
  final String title;
  final String description;
  final bool completed;

  Task({required this.id, required this.title, required this.description, required this.completed});
}
```

## Implementing Data Synchronization

Now, let's jump into the exciting part - implementing data synchronization across devices. We will create a `TaskList` widget that displays a list of tasks and allows users to add and update tasks. This widget will be a StatelessWidget.

First, import the necessary packages:

```dart
import 'package:firebase_database/firebase_database.dart';
import 'package:flutter/material.dart';
```

Next, create a class called `TaskList`:

```dart
class TaskList extends StatelessWidget {
  final DatabaseReference _databaseReference = FirebaseDatabase.instance.reference().child('tasks');

  @override
  Widget build(BuildContext context) {
    return StreamBuilder<Event>(
      stream: _databaseReference.onValue,
      builder: (context, snapshot) {
        if (snapshot.hasData) {
          List<Task> tasks = [];
          DataSnapshot dataSnapshot = snapshot.data!.snapshot;

          dataSnapshot.value.forEach((key, value) {
            tasks.add(Task(
              id: key,
              title: value['title'],
              description: value['description'],
              completed: value['completed'],
            ));
          });

          return ListView.builder(
            itemCount: tasks.length,
            itemBuilder: (context, index) {
              Task task = tasks[index];
              return ListTile(
                title: Text(task.title),
                subtitle: Text(task.description),
                trailing: Checkbox(
                  value: task.completed,
                  onChanged: (value) {
                    _databaseReference.child(task.id).update({'completed': value});
                  },
                ),
              );
            },
          );
        } else {
          return Center(child: CircularProgressIndicator());
        }
      },
    );
  }
}
```

In the `build` method of the `TaskList` widget, we use a `StreamBuilder` to listen to changes in the Firebase Realtime Database. Whenever there is a change in the data, the builder function is called, allowing us to update the UI accordingly.

Inside the builder function, we retrieve the tasks data from the snapshot and populate a list of `Task` objects. We then use a `ListView.builder` to display the tasks in a scrollable list with checkboxes to mark tasks as completed. When a checkbox is toggled, we update the corresponding task's completion status in the database.

## Adding the TaskList Widget

To use the `TaskList` widget, simply add it to your app's widget tree:

```dart
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Data Sync',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Task List'),
        ),
        body: TaskList(),
      ),
    );
  }
}
```

And that's it! You now have a data synchronization mechanism in place across devices using Firebase Realtime Database in your Flutter app. Users can add tasks, update their completion status, and see the changes reflected instantly on all their devices.

#flutter #dataSync