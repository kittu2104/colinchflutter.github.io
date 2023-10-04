---
layout: post
title: "Using input/output data with WorkManager in Flutter"
description: " "
date: 2023-10-01
tags: [workmanager]
comments: true
share: true
---

WorkManager is a powerful library in Flutter that allows you to perform background tasks efficiently. In addition to running tasks in the background, WorkManager also enables you to pass input and receive output data from these tasks. This flexibility provides a way to transfer data between your main application and background tasks seamlessly. In this article, we'll explore how to use input/output data with WorkManager in Flutter.

## Adding WorkManager Dependencies

To get started, you need to add the WorkManager dependency to your Flutter project. Open your `pubspec.yaml` file and add the following lines:

```yaml
dependencies:
  workmanager: ^0.4.0
```

Then, run the command `flutter pub get` to fetch the newly added package.

## Implementing a Background Task

Next, let's create a background task using the WorkManager library. Create a new file, for example `background_task.dart`, and add the following code:

```dart
import 'dart:async';
import 'package:workmanager/workmanager.dart';

void callbackDispatcher() {
  Workmanager.executeTask((task, inputData) {
    // Perform background task and return outputData
    String outputData = performBackgroundTask(inputData);
    return Future.value(outputData);
  });
}

String performBackgroundTask(Map<String, dynamic> inputData) {
  // Access input data and perform necessary operations
  String input = inputData['input'];
  
  // Perform the task and return output data
  String output = // Perform background task with input data
  
  return output;
}

void registerBackgroundTask() {
  Workmanager.initialize(callbackDispatcher, isInDebugMode: true);
  Workmanager.registerPeriodicTask(
    "backgroundTask",
    // Other configuration parameters...
    inputData: {
      'input': 'Example Input Data',
    },
  );
}
```

In the above code, we define the `callbackDispatcher` function that will be invoked whenever the background task is triggered. Inside the `callbackDispatcher`, we use the `executeTask` method to perform the actual background task. The `performBackgroundTask` function takes the input data passed from the main application, performs the task, and returns the output data.

To register the background task, call the `registerBackgroundTask` function, which initializes the WorkManager and registers the periodic task. Don't forget to import the `workmanager` package at the top of your file.

## Publishing Input Data

Once you have set up the background task, you can publish input data from your main application to be used by the background task. To do this, call the following code from your main application:

```dart
import 'package:workmanager/workmanager.dart';

void sendDataToBackgroundTask() {
  Workmanager().sendData(
    {'input': 'Example Input Data'},
  );
}
```

In the above code, we utilize the `sendData` method provided by WorkManager to send the input data as a key-value map to the background task. Make sure to import the `workmanager` package in your main application as well.

## Receiving Output Data

To receive output data from the background task in your main application, you need to register a callback. Below is an example code snippet to achieve this:

```dart
import 'package:workmanager/workmanager.dart';

void registerBackgroundTaskCallback() {
  Workmanager().setTaskCompletedListener((taskId, outputData) {
    // Process the outputData received from the background task
    // e.g., update the UI with the output data
    print("Received Output Data: $outputData");
  });
}
```

In the above code, we use the `setTaskCompletedListener` method provided by WorkManager to register a callback. The `outputData` parameter contains the data returned by the background task.

## Conclusion

By utilizing input/output data with WorkManager in Flutter, you can seamlessly pass data between your main application and background tasks. This opens up possibilities for performing complex operations in the background and updating your UI with the output data. Explore the WorkManager library's documentation to dive deeper into its capabilities and unlock the full potential of background tasks in your Flutter applications.

#flutter #workmanager