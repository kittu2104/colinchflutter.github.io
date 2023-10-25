---
layout: post
title: "How to run tasks in the background in Flutter?"
description: " "
date: 2023-10-25
tags: [backgroundTasks]
comments: true
share: true
---

In some cases, you may need to run tasks in the background in your Flutter application. This could be useful for performing long-running operations, such as fetching data from an API or processing large amounts of data.

Flutter provides a plugin called `flutter_background_service` that allows you to run tasks in the background. It provides a simple and easy-to-use API for starting and stopping background tasks.

## Installation

To use the `flutter_background_service` plugin, you need to add it to your `pubspec.yaml` file. Open the file and add the following line under `dependencies`:

```yaml
dependencies:
  flutter_background_service: ^1.2.0
```

Save the file and run `flutter pub get` to fetch the plugin.

## Implementing background tasks

Once you have installed the `flutter_background_service` plugin, you can start implementing background tasks in your Flutter application.

First, import the necessary packages:

```dart
import 'package:flutter_background_service/flutter_background_service.dart';
import 'package:flutter/material.dart';
```

Next, you need to override the `start` method of your main `MyApp` class. This is where you define the logic for your background task. Here's an example:

```dart
void main() {
  WidgetsFlutterBinding.ensureInitialized();
  FlutterBackgroundService.initialize(onStart);
  runApp(MyApp());
}

void onStart() {
  WidgetsFlutterBinding.ensureInitialized();
  FlutterBackgroundService().sendData({
    "action": "backgroundTask",
    "text": "Running in the background...",
  });
  Timer.periodic(Duration(seconds: 5), (timer) {
    // Perform your background task here
    // You can fetch data from API, process data, etc.
    FlutterBackgroundService().sendData({
      "action": "backgroundTask",
      "text": "Background task is running...",
    });
  });
}
```

In this example, we are using a `Timer` to run a background task every 5 seconds. You can modify this logic to suit your needs.

## Handling background tasks in your UI

To handle the background tasks in your UI, you can listen for the messages sent by the background task using a `StreamBuilder`.

```dart
StreamBuilder<Map<String, dynamic>>(
  stream: FlutterBackgroundService().onDataReceived,
  builder: (context, snapshot) {
    if (!snapshot.hasData) {
      return CircularProgressIndicator();
    }
    final data = snapshot.data;
    final text = data['text'];
    return Text(text);
  },
)
```

In this example, we are displaying the text sent by the background task in a `Text` widget. You can customize the UI according to your requirements.

## Running the background task

To start the background task, you can call the `FlutterBackgroundService().start()` method. You can trigger this from a button press or any other UI interaction.

```dart
FlatButton(
  onPressed: () {
    FlutterBackgroundService().start();
  },
  child: Text('Start Background Task'),
)
```

## Stopping the background task

To stop the background task, you can call the `FlutterBackgroundService().stop()` method. You can trigger this from a button press or any other UI interaction.

```dart
FlatButton(
  onPressed: () {
    FlutterBackgroundService().stop();
  },
  child: Text('Stop Background Task'),
)
```

## Conclusion

Running tasks in the background is an important feature for many Flutter applications. By using the `flutter_background_service` plugin, you can easily run background tasks and handle them in your UI. This allows you to perform long-running operations without blocking the main thread and provides a smoother user experience.

Make sure to explore the official documentation of the `flutter_background_service` plugin for more advanced usage and features.

**#flutter #backgroundTasks**