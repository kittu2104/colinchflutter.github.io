---
layout: post
title: "Working with broadcast receivers in WorkManager for Flutter"
description: " "
date: 2023-10-01
tags: [flutter, broadcastreceivers, workmanager, flutterdevelopment]
comments: true
share: true
---

Flutter is a powerful framework for building cross-platform applications. When it comes to running background tasks in your Flutter app, the WorkManager plugin provides a convenient solution. One of the key features of WorkManager is the ability to work with broadcast receivers, which allow your app to receive system-level events and perform actions accordingly. In this article, we will explore how to use broadcast receivers with WorkManager in a Flutter app.

## What is a Broadcast Receiver?

A broadcast receiver is a component of an Android app that listens for and responds to system-wide broadcast messages. These messages can be sent by the operating system or other apps on the device. By registering a broadcast receiver in your app, you can receive these messages and trigger appropriate actions.

## Adding Dependencies

To get started, you'll need to add the WorkManager and WorkManager Flutter plugins to your Flutter project. Open your `pubspec.yaml` file and add the following dependencies:

```yaml
dependencies:
  workmanager: ^0.4.0
  workmanager_flutter: ^0.5.0
```

After adding the dependencies, run `flutter pub get` to download and activate them in your project.

## Registering a Broadcast Receiver

To listen for system-wide broadcast messages in your Flutter app, you need to create a broadcast receiver class and register it in your `AndroidManifest.xml` file. Here's an example of how you can do this:

```xml
<receiver android:name=".MyBroadcastReceiver"
    android:exported="true"
    android:enabled="true">
    <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED" />
        <action android:name="android.intent.action.MY_CUSTOM_ACTION" />
    </intent-filter>
</receiver>
```

In the example above, we define a broadcast receiver called `MyBroadcastReceiver` and specify two intent filters: `BOOT_COMPLETED` and `MY_CUSTOM_ACTION`. These intent filters determine the type of broadcast messages that the receiver will pick up. Feel free to modify the intent filters based on your specific needs.

## Handling Broadcast Messages with WorkManager

To handle the broadcast messages received by your broadcast receiver with WorkManager, you can create a background task using the WorkManager plugin. Here's an example of how you can define a simple background task that runs when the broadcast receiver receives a message:

```dart
import 'package:workmanager/workmanager.dart';

void callbackDispatcher() {
  Workmanager.executeTask((task, inputData) {
    // Handle the broadcast message
    if (task == "broadcastTask") {
      // Perform the desired action
      print("Broadcast message received!");
    }
    return Future.value(true);
  });
}

void registerBroadcastReceiver() {
  Workmanager.initialize(
    callbackDispatcher,
    isInDebugMode: false, // Set this to true for debugging
  );
  Workmanager.registerOneOffTask(
    "broadcastTask",
    "broadcastTaskTag",
    initialDelay: Duration(seconds: 0),
  );
}
```

In the example above, we define a function called `callbackDispatcher()` that will be triggered when the broadcast message is received. Inside the callback, we check the type of task and perform the desired action. In this case, we simply print a message to the console.

To register the broadcast receiver and start the background task, we call the `registerBroadcastReceiver()` function. This will initialize WorkManager and register the `broadcastTask` with the specified tag. The background task will be triggered immediately once the broadcast message is received.

## Conclusion

Using broadcast receivers with WorkManager in Flutter opens up a wide range of possibilities for handling system-level events and performing actions in your app. By registering a broadcast receiver and leveraging the power of WorkManager, you can efficiently run background tasks and keep your app responsive and up-to-date.

Remember to add the necessary dependencies and register the broadcast receiver in your `AndroidManifest.xml` file to make it work seamlessly. Happy coding!

#flutter #broadcastreceivers #workmanager #flutterdevelopment