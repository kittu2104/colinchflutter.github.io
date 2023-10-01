---
layout: post
title: "Implementing one-time scheduled tasks with WorkManager in Flutter"
description: " "
date: 2023-10-01
tags: [Flutter, WorkManager]
comments: true
share: true
---

In mobile app development, it's common to have tasks that need to be executed at a specific time or interval. Whether it's a reminder notification, data synchronization, or any other periodic task, scheduling it can be challenging, especially when dealing with app lifecycle and system restrictions.

**WorkManager** is a powerful library in Flutter that provides a flexible way to schedule and manage background tasks. It handles system optimizations and ensures that your tasks are executed even if the app is not running.

In this tutorial, we will explore how to use WorkManager to schedule one-time tasks in Flutter.

## Installation

First, you need to add the `flutter_workmanager` package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_workmanager: ^0.3.0
```

Then, run the command `flutter pub get` to install the package.

## Basic Usage

To use WorkManager, you need to create a **Task**. A task represents the work to be done, such as sending an API request, updating the database, or showing a notification. Here's an example:

```dart
import 'package:flutter_workmanager/flutter_workmanager.dart';

void callbackDispatcher() {
  Workmanager.executeTask((task, inputData) {
    // Your task logic goes here
    return Future.value(true);
  });
}

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Workmanager.initialize(callbackDispatcher);
  Workmanager.registerOneOffTask(
    'myTask',
    'myTaskTag',
    inputData: {},
  );
  runApp(MyApp());
}
```

In the example above, we define a callback function `callbackDispatcher`, which will be called when the task is executed. The `executeTask` function wraps our task logic, and we use `Future.value(true)` to indicate that the task has completed successfully.

Inside the `main` function, we initialize WorkManager using `Workmanager.initialize(callbackDispatcher)` to establish the callback function. Then, we register a one-off task using `Workmanager.registerOneOffTask`, providing a unique task name (`myTask`), a tag (`myTaskTag`), and any necessary `inputData`.

## Handling the Task Logic

Now that we have the skeleton in place, let's add our actual task logic. Below is an example of sending an API request:

```dart
import 'package:flutter_workmanager/flutter_workmanager.dart';
import 'package:http/http.dart' as http;

void callbackDispatcher() {
  Workmanager.executeTask((task, inputData) async {
    if (task == 'myTask') {
      await sendApiRequest();
      return Future.value(true);
    }
    return Future.value(false);
  });
}

Future<void> sendApiRequest() async {
  final response = await http.get(Uri.parse('https://example.com/api/data'));
  // Process the response
}
```

In this example, we add a condition in the `callbackDispatcher` to check the task name before executing the logic. If the task name matches, we call the `sendApiRequest` function. After the request is made, you can process the response as needed.

## Testing the Task

To test the task locally, you can use the `flutter_workmanager` package's `Workmanager.debug` method. This sends a test event to the callback function, simulating the execution of the task.

```dart
import 'package:flutter_workmanager/flutter_workmanager.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Workmanager.initialize(callbackDispatcher);
  Workmanager.debug();
  runApp(MyApp());
}
```

By running the app with `Workmanager.debug` enabled, the callback function will be triggered, and you can verify that the task logic is working as expected.

Now you have learned how to use WorkManager to schedule one-time tasks in Flutter. This can greatly enhance the functionality of your app by allowing you to perform background tasks at specific times or intervals. Remember to optimize your tasks and consider system limitations to ensure smooth execution. Happy coding!

## #Flutter #WorkManager