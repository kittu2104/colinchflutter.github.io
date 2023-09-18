---
layout: post
title: "Creating a to-do list app with alarm notifications using Flutter Alarm Manager"
description: " "
date: 2023-09-18
tags: [AlarmManager]
comments: true
share: true
---

In this tutorial, we will learn how to create a to-do list app using Flutter and implement alarm notifications using the Flutter Alarm Manager package.

## Prerequisites

Before we begin, make sure you have the following:

- Flutter SDK installed on your machine
- Flutter project set up

## Setting Up

First, open your terminal and navigate to the root directory of your Flutter project. Run the following command to add the Flutter Alarm Manager package to your project:

```
flutter pub add flutter_local_notifications
```

Next, import the `flutter_local_notifications` package in your `main.dart` file:

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';
```

## Building the To-Do List

Now, let's create a simple to-do list.

```dart
import 'package:flutter/material.dart';

class TodoListApp extends StatefulWidget {
  @override
  _TodoListAppState createState() => _TodoListAppState();
}

class _TodoListAppState extends State<TodoListApp> {
  List<String> todos = [];
  
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("To-Do List"),
      ),
      body: ListView.builder(
        itemCount: todos.length,
        itemBuilder: (context, index) {
          var todo = todos[index];
          return ListTile(
            title: Text(todo),
          );
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          showDialog(
            context: context,
            builder: (context) {
              String newTodo = '';
              return AlertDialog(
                title: Text('Add Todo'),
                content: TextField(
                  onChanged: (value) {
                    newTodo = value;
                  },
                ),
                actions: [
                  ElevatedButton(
                    onPressed: () {
                      Navigator.pop(context);
                      setState(() {
                        todos.add(newTodo);
                      });
                    },
                    child: Text('Add'),
                  ),
                ],
              );
            },
          );
        },
        child: Icon(Icons.add),
      ),
    );
  }
}
```

## Implementing Alarm Notifications

Now, let's add alarm notifications to our to-do list app using the Flutter Alarm Manager package.

```dart
class _TodoListAppState extends State<TodoListApp> {
  FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin =
      FlutterLocalNotificationsPlugin();

  @override
  void initState() {
    super.initState();
    var initializationSettingsAndroid =
        AndroidInitializationSettings('@mipmap/ic_launcher');
    var initializationSettingsIOS = IOSInitializationSettings();
    var initializationSettings = InitializationSettings(
        android: initializationSettingsAndroid, iOS: initializationSettingsIOS);
    flutterLocalNotificationsPlugin.initialize(initializationSettings,
        onSelectNotification: onSelectNotification);
  }

  Future onSelectNotification(String? payload) async {
    if (payload != null) {
      debugPrint('notification payload: $payload');
    }
  }

  Future<void> _scheduleNotification(DateTime dateTime, String todo) async {
    var scheduledNotificationDateTime =
        DateTime.now().add(Duration(seconds: 5));

    var androidPlatformChannelSpecifics = AndroidNotificationDetails(
      'your channel id',
      'your channel name',
      'your channel description',
    );
    var iOSPlatformChannelSpecifics = IOSNotificationDetails();
    var platformChannelSpecifics = NotificationDetails(
        android: androidPlatformChannelSpecifics,
        iOS: iOSPlatformChannelSpecifics);

    await flutterLocalNotificationsPlugin.schedule(
        0, 'Reminder', 'Reminder to complete $todo', scheduledNotificationDateTime, platformChannelSpecifics);
  }

  // Rest of the code...
}
```

Now, whenever a new to-do item is added to the list, we can schedule a notification using the `_scheduleNotification` method.

```dart
floatingActionButton: FloatingActionButton(
  onPressed: () {
    showDialog(
      context: context,
      builder: (context) {
        String newTodo = '';

        return AlertDialog(
          title: Text('Add Todo'),
          content: TextField(
            onChanged: (value) {
              newTodo = value;
            },
          ),
          actions: [
            ElevatedButton(
              onPressed: () {
                Navigator.pop(context);
                setState(() {
                  todos.add(newTodo);
                  _scheduleNotification(DateTime.now(), newTodo);
                });
              },
              child: Text('Add'),
            ),
          ],
        );
      },
    );
  },
  child: Icon(Icons.add),
),
```

## Conclusion

Congratulations! You have successfully created a to-do list app with alarm notifications using the Flutter Alarm Manager package. You can now explore additional features such as customizing notifications or adding the ability to mark tasks as complete. Have fun building your own productivity app! #Flutter #AlarmManager