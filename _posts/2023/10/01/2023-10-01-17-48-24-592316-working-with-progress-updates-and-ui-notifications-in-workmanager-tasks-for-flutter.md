---
layout: post
title: "Working with progress updates and UI notifications in WorkManager tasks for Flutter"
description: " "
date: 2023-10-01
tags: [flutter, backgroundtasks]
comments: true
share: true
---

In Flutter, background tasks can be efficiently managed using WorkManager. It provides a way to run tasks even when the app is not active or has been closed. WorkManager makes it easy to perform long-running operations, such as API calls or file downloads, without blocking the user interface.

One crucial aspect of background tasks is providing progress updates and UI notifications to keep the user informed about the task's progress. In this blog post, we will explore how to accomplish this using WorkManager in Flutter.

## Setting Up WorkManager

Before diving into progress updates and UI notifications, let's set up WorkManager in a Flutter project.

First, add the workmanager package to your `pubspec.yaml` file:

```yaml
dependencies:
  workmanager: ^0.4.0
```

Next, initialize WorkManager and register your task in the `main` function of your `main.dart` file:

```dart
import 'package:flutter/material.dart';
import 'package:workmanager/workmanager.dart';

void callbackDispatcher() {
  Workmanager.executeTask((task, inputData) {
    // Your task logic here
    return Future.value(true);
  });
}

void main() {
  WidgetsFlutterBinding.ensureInitialized();
  Workmanager.initialize(callbackDispatcher);
  Workmanager.registerPeriodicTask(
    "taskName",
    "taskIdentifier",
    frequency: Duration(minutes: 15),
  );
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'WorkManager Demo',
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('WorkManager Demo')),
      body: Center(child: Text('Background Task Demo')),
    );
  }
}
```

## Updating Progress of a Task

To update the progress of a background task, you can make use of Flutter's event system. WorkManager allows you to pass data to the background task using `inputData`. We can utilize this to send progress updates from the task back to the UI.

Here's an example of how to update the progress of a task:

```dart
void callbackDispatcher() {
  Workmanager.executeTask((task, inputData) async {
    if (task == "taskName") {
      for (int i = 0; i <= 100; i += 10) {
        await Workmanager().updateProgress(
          progress: i,
          taskKey: inputData["taskKey"],
        );
        await Future.delayed(Duration(seconds: 1));
      }
      return Future.value(true);
    }
    return Future.error("Unknown task");
  });
}
```

In the above code snippet, we iterate over the progress values from 0 to 100 and update the progress using `updateProgress` method. We also need to provide the `taskKey` received in `inputData` to associate the progress update with the correct task.

## Displaying UI Notifications

To display UI notifications when the background task completes or when there is a progress update, you can use the flutter_local_notifications package. This package provides a platform-agnostic way to show notifications in Flutter.

Here's an example of how to display a notification on task completion:

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';

final FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin =
    FlutterLocalNotificationsPlugin();

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await flutterLocalNotificationsPlugin.initialize(
    InitializationSettings(
      android: AndroidInitializationSettings('app_icon'),
    ),
  );
  // Rest of the code...
}

void callbackDispatcher() {
  Workmanager.executeTask((task, inputData) async {
    if (task == "taskName") {
      // Your task logic here

      // Display notification on completion
      const AndroidNotificationDetails androidPlatformChannelSpecifics =
          AndroidNotificationDetails('channelId', 'channelName',
              channelDescription: 'Your channel description',
              importance: Importance.max,
              priority: Priority.high);
      const NotificationDetails platformChannelSpecifics =
          NotificationDetails(android: androidPlatformChannelSpecifics);
      await flutterLocalNotificationsPlugin.show(
        0,
        'Task Completed',
        'Your background task has completed',
        platformChannelSpecifics,
      );

      return Future.value(true);
    }
    return Future.error("Unknown task");
  });
}
```

In the above code snippet, we initialize the `flutter_local_notifications` plugin and show a notification using `show` method when the background task completes.

## Conclusion

By leveraging WorkManager, we can efficiently perform background tasks in Flutter. With the ability to update progress and display UI notifications, users can stay informed about the task's status even when the app is not active. This enhances the overall user experience and makes your app more robust.

Remember to handle permissions, such as network access and foreground services, for your specific background task requirements. WorkManager offers various configuration options to cater to different use cases, making it a powerful tool for managing background tasks in Flutter applications.

#flutter #backgroundtasks