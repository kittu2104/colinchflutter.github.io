---
layout: post
title: "How to get device height using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [MediaQuery]
comments: true
share: true
---

Introduction:
In Flutter, it's important to ensure that your app's UI adapts well to different device sizes. One way to achieve this is by using the `MediaQuery` class to get important information about the device's screen, such as the height. In this blog post, we will learn how to easily retrieve and utilize the device height in Flutter using the `MediaQuery` class.

Content:
To get the device height using `MediaQuery` in Flutter, follow these steps:

Step 1: Import the necessary packages.
```dart
import 'package:flutter/material.dart';
```

Step 2: Create a method to get the device height.
```dart
double getDeviceHeight(BuildContext context) {
  return MediaQuery.of(context).size.height;
}
```

Step 3: Utilize the method in your Flutter application.
```dart
class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    double deviceHeight = getDeviceHeight(context);

    return Container(
      height: deviceHeight * 0.8, // Example usage to set container height
      color: Colors.blue,
      child: Center(
        child: Text(
          'Device Height: ${deviceHeight.toStringAsFixed(2)}',
          style: TextStyle(
            fontSize: 20.0,
            fontWeight: FontWeight.bold,
            color: Colors.white,
          ),
        ),
      ),
    );
  }
}
```

Explanation:
- In step 2, we define a method called `getDeviceHeight` that takes the `BuildContext` as a parameter and returns the device height using `MediaQuery`.
- In step 3, we utilize the `getDeviceHeight` method within a `MyWidget` class. Here, we use the retrieved height to set the height of a container and display the device height as text in the center of the container.

Conclusion:
In this blog post, we learned how to get the device height using `MediaQuery` in Flutter. By utilizing the `getDeviceHeight` method, you can ensure that your app's UI adapts well to various screen sizes. Remember to import the necessary packages and utilize the method as per your application's requirements.

#Flutter #MediaQuery