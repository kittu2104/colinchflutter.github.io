---
layout: post
title: "Running background services for real-time updates in Flutter"
description: " "
date: 2023-10-25
tags: []
comments: true
share: true
---

In mobile app development, having real-time updates is a common requirement. Whether it's updating chat messages, live sports scores, or stock market data, it's crucial to have a way to keep the app updated with the latest information. In Flutter, one way to achieve this is by running background services that handle real-time updates.

## Understanding background services in Flutter

In Flutter, background services allow you to run tasks in the background, even when the app is not actively running. Background services are useful for handling tasks that require periodic or continuous updates, such as fetching data from an API or updating the user interface.

## Using the Workmanager package

To run background services in Flutter, we can make use of the **Workmanager** package. This package provides an easy way to schedule tasks and run them periodically in the background. 

To get started, add the **workmanager** package to your `pubspec.yaml` file:

```yaml
dependencies:
  workmanager: ^0.4.0
```

Next, import the package into your Dart file:

```dart
import 'package:workmanager/workmanager.dart';
```

## Scheduling periodic tasks

To schedule a periodic task, we need to initialize the `Workmanager` package and register a callback function that will be called periodically. The callback function should contain the logic for updating the app with the latest information.

Here's an example of scheduling a periodic task that runs every 15 minutes:

```dart
void main() {
  Workmanager.initialize(callbackDispatcher, isInDebugMode: true);
  Workmanager.registerPeriodicTask(
    "1",
    "background_task",
    frequency: Duration(minutes: 15),
  );
}

void callbackDispatcher() {
  Workmanager.executeTask((task, inputData) {
    // Handle the task here, such as fetching data from an API
    // or updating the user interface with the latest information
    return Future.value(true);
  });
}
```

## Running background services on Android and iOS

To ensure that background services work on both Android and iOS devices, make sure to add the necessary configuration to the respective platform files.

For Android, add the following permission to your `AndroidManifest.xml` file:

```xml
<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
```

For iOS, open the `AppDelegate.swift` file and add the following code inside the `application(_:didFinishLaunchingWithOptions:)` method:

```swift
UIApplication.shared.setMinimumBackgroundFetchInterval(
    UIApplication.backgroundFetchIntervalMinimum
)
```

## Conclusion

Running background services for real-time updates in Flutter is essential for keeping your app up-to-date with the latest information. By using the **Workmanager** package and scheduling periodic tasks, you can easily handle tasks that require continuous updates.

Remember to test your background services on both Android and iOS devices to ensure they work as expected. With Flutter's powerful capabilities, you can create robust and responsive apps that provide real-time updates to your users.

# References
- [Workmanager package](https://pub.dev/packages/workmanager)
- [Flutter documentation: Background Execution](https://flutter.dev/docs/development/packages-and-plugins/background-processes)