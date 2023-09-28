---
layout: post
title: "Creating a responsive notification banner using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [responsivedesign]
comments: true
share: true
---

In this blog post, we will explore how to create a responsive notification banner using `MediaQuery` in Flutter. This will allow the notification banner to adjust its size and layout based on the screen size and orientation of the device.

## What is MediaQuery?

`MediaQuery` is a class in Flutter that contains information about the current media, such as the screen size, device pixel ratio, and orientation. It allows us to create responsive layouts by adapting the UI based on the device's capabilities.

## Implementing the Notification Banner

To create a responsive notification banner, we will follow these steps:

1. Create a new Flutter project or open an existing one.

2. Inside the `lib` directory, create a new file called `notification_banner.dart`.

3. Import the necessary packages:
```dart
import 'package:flutter/material.dart';
```

4. Create a stateless widget called `NotificationBanner`:
```dart
class NotificationBanner extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      height: MediaQuery.of(context).size.height * 0.1,
      color: Colors.blue,
      child: Center(
        child: Text(
          'New Notification',
          style: TextStyle(
            color: Colors.white,
            fontSize: 16.0,
            fontWeight: FontWeight.bold,
          ),
        ),
      ),
    );
  }
}
```

5. In the main file, add the `NotificationBanner` widget to the app's widget tree:
```dart
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Notification Banner Example',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Notification Banner Example'),
        ),
        body: Column(
          children: [
            // Rest of the app's content
            // ...
            NotificationBanner(), // Add the notification banner here
          ],
        ),
      ),
    );
  }
}
```

6. Run the app and see the responsive notification banner in action! The banner's height will adjust based on the device's screen size.

## Conclusion

By utilizing `MediaQuery` in Flutter, we can easily create responsive notification banners that adapt to different screen sizes and orientations. This allows for a better user experience and ensures that the notification banner is prominently displayed on all devices.

#flutter #responsivedesign