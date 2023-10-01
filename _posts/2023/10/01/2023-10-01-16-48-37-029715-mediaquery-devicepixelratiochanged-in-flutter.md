---
layout: post
title: "MediaQuery devicePixelRatioChanged in Flutter"
description: " "
date: 2023-10-01
tags: [Flutter, MediaQuery]
comments: true
share: true
---

In Flutter, `MediaQuery` is a powerful class that provides access to the media information and device characteristics. It allows developers to build responsive UIs and adapt their app's layout based on various factors like screen size, orientation, and pixel density.

One of the notable features of the `MediaQuery` class is the `devicePixelRatioChanged` callback. This callback is invoked whenever there is a change in the device's pixel density, allowing you to respond to such changes and perform necessary actions.

To listen for the `devicePixelRatioChanged` event, you need to wrap your widget with a `NotificationListener` and provide the appropriate notification type:

```dart
NotificationListener<MediaQueryInfo>(
  onNotification: (notification) {
    if (notification is MediaQueryInfo) {
      if (notification.type == MediaQueryType.devicePixelRatioChanged) {
        // Perform actions on device pixel density change
        // For example, update UI elements or redraw the screen
        // ...
      }
    }
    return true;
  },
  child: YourWidget(),
);
```

In this example code snippet, `MediaQueryInfo` is a custom notification class representing media query events. You can create it by extending the `Notification` class:

```dart
class MediaQueryInfo extends Notification {
  final MediaQueryType type;

  MediaQueryInfo(this.type);
}

enum MediaQueryType {
  devicePixelRatioChanged,
  // Add other media query types...
}
```

Once you have set up the notification listener and notification classes, you can implement any desired actions when the `devicePixelRatioChanged` event occurs. This can be useful, for example, when you want to re-render your UI components to adapt to a new pixel density or update certain UI elements based on the screen resolution.

Remember to dispose of the listeners when they are no longer needed to avoid memory leaks. You can do this by overriding the `dispose` method in your widget and removing the listener:

```dart
@override
void dispose() {
  // Remove the listener
  notificationListener?.dispose();
  super.dispose();
}
```

By utilizing the `devicePixelRatioChanged` callback in `MediaQuery`, you can ensure that your Flutter app provides a smooth and responsive user experience even when the device's pixel density changes. Stay up-to-date with the latest industry trends and adapt your app's UI accordingly to deliver a delightful user interface.

**#Flutter #MediaQuery**