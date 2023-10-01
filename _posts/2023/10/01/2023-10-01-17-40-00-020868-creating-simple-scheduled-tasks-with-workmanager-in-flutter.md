---
layout: post
title: "Creating simple scheduled tasks with WorkManager in Flutter"
description: " "
date: 2023-10-01
tags: [flutter, workmanager]
comments: true
share: true
---

With the growing complexity of mobile applications, it has become essential to offload certain tasks to the background to ensure a smooth user experience. WorkManager is a powerful library that helps in scheduling and managing tasks in the background in Flutter.

## What is WorkManager?

WorkManager is a part of the Android Jetpack library suite and provides a unified API to schedule background tasks that need to run even if the app is closed or the device is rebooted. It can be used to handle tasks like data syncing, uploading files, or sending notifications.

## Setting up WorkManager in Flutter

To start using WorkManager, you'll need to add the `workmanager` package to your Flutter project. You can do this by adding the following dependency to your `pubspec.yaml` file:

```
dependencies:
  workmanager: ^x.x.x
```

Replace `x.x.x` with the latest version of the `workmanager` package.

After adding the dependency, run `flutter packages get` to fetch the package and its dependencies.

## Scheduling tasks with WorkManager

To schedule a task with WorkManager, you need to define a background callback function that will be executed when the task is triggered. This function should do the necessary work in the background.

Here's an example of how you can schedule a simple periodic task with WorkManager:

```dart
import 'package:workmanager/workmanager.dart';

void callbackDispatcher() {
  Workmanager.executeTask((task, inputData) {
    // Perform your background task here
    print("Background task executed");

    return Future.value(true);
  });
}

void main() {
  Workmanager.initialize(
    callbackDispatcher,
    isInDebugMode: true,
  );
  
  Workmanager.registerPeriodicTask(
    "periodicTask",
    "simplePeriodicTask",
    frequency: Duration(hours: 1),
  );
}
```

In the above example, `callbackDispatcher()` is the background callback function that will be executed whenever the scheduled task is triggered. Inside this function, you can perform your desired background task.

The `main()` function initializes WorkManager with the callbackDispatcher and registers a periodic task named `periodicTask` with a frequency of one hour. This task will execute the `callbackDispatcher` function every hour in the background.

## Conclusion

WorkManager is a powerful tool for managing background tasks in Flutter. It allows you to offload time-consuming operations and ensures a smoother user experience. By following this guide, you should now have a better understanding of how to schedule simple tasks with WorkManager in your Flutter applications.

#flutter #workmanager