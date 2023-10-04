---
layout: post
title: "useNotificationListener hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: [FlutterHooks]
comments: true
share: true
---

In Flutter Hooks, there is a useful hook called `useNotificationListener` which allows you to easily handle system notifications in your Flutter application. This hook can be used to listen for various system notifications like when your application enters or exits the background, when the device's orientation changes, or when the system keyboard is shown or hidden.

## Usage

To use the `useNotificationListener` hook, you first need to import it from the `flutter_hooks` package:

```dart
import 'package:flutter_hooks/flutter_hooks.dart';
```

Next, you can use the hook within a widget's build method like this:

```dart
Widget build(BuildContext context) {
  useNotificationListener(
    onNotification: (notification) {
      // Handle the system notification here.
    },
    // Add any necessary options here.
  );

  // Rest of your widget code.
}
```

## Parameters

The `useNotificationListener` hook accepts the following parameters:

- `onNotification`: A callback function that gets triggered when a system notification is received. This function takes a `Notification` object as its parameter, which can be used to determine the specific type of notification.

- `options` (optional): An instance of `NotificationListenerOptions` that allows you to specify additional options for the listener. These options include `NotificationListenerCallbackMode`, which determines when the callback should be invoked, and `callbacks` which can be used to specify callbacks for specific types of notifications.

## Example

Let's say you want to show a SnackBar whenever the device's orientation changes. You can achieve this using the `useNotificationListener` hook as follows:

```dart
Widget build(BuildContext context) {
  useNotificationListener(
    onNotification: (notification) {
      if (notification is OrientationChangedNotification) {
        ScaffoldMessenger.of(context).showSnackBar(
          SnackBar(
            content: Text('Device orientation changed'),
          ),
        );
      }
    },
  );

  return Scaffold(
    appBar: AppBar(
      title: Text('Flutter Hooks Example'),
    ),
    body: Center(
      child: Text('Hello World'),
    ),
  );
}
```

In the above example, whenever the device's orientation changes, the `onNotification` callback is triggered, showing a SnackBar with the message "Device orientation changed".

## Conclusion

The `useNotificationListener` hook in Flutter Hooks provides a convenient way to handle system notifications in your Flutter application. By using this hook, you can easily listen for system events and perform custom actions based on those events, enhancing the functionality of your app. So, go ahead and explore the possibilities of `useNotificationListener` in your Flutter projects! #Flutter #FlutterHooks