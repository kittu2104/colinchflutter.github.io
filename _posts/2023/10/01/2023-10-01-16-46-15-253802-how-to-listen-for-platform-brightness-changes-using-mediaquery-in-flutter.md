---
layout: post
title: "How to listen for platform brightness changes using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [flutter, mediquery]
comments: true
share: true
---

One of the great features of Flutter is its ability to adapt to the user's device preferences. This includes adjusting the brightness level of the screen. In this blog post, we will explore how to use the `MediaQuery` class in Flutter to listen for platform brightness changes.

## Step 1: Import the necessary packages

To get started, you need to import the `flutter/material.dart` package. Open your Dart file and add the following import statement at the top:

```dart
import 'package:flutter/material.dart';
```

## Step 2: Use a `MediaQuery` widget

Next, you need to wrap your main widget with a `MediaQuery` widget. This allows you to access the device's platform brightness level. Here's an example of how to use the `MediaQuery` widget:

```dart
class BrightnessListener extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MediaQuery(
      data: MediaQueryData(),
      child: YourMainWidget(),
    );
  }
}

class YourMainWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // Here you can access the platform brightness value
    Brightness brightness = MediaQuery.of(context).platformBrightness;
    
    // Do something with the brightness value
    
    return Scaffold(
      // Your UI code
    );
  }
}
```

## Step 3: Listen for brightness changes

To listen for changes in the platform brightness, you need to wrap the widget that needs to react to the brightness changes with a `Builder` widget. Here's an example:

```dart
class BrightnessListener extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MediaQuery(
      data: MediaQueryData(),
      child: Builder(
        builder: (BuildContext context) {
          // Here you can access the platform brightness value
          Brightness brightness = MediaQuery.of(context).platformBrightness;
          
          // Do something with the brightness value
          
          return YourMainWidget();
        },
      ),
    );
  }
}
```

Now, whenever the platform brightness changes, the widget wrapped in the `Builder` widget will rebuild, allowing you to update the UI based on the new brightness value.

## Conclusion

By using the `MediaQuery` class in Flutter, you can easily listen for platform brightness changes and adjust your UI accordingly. This allows you to create apps that adapt to the user's device preferences, providing a seamless user experience. So go ahead and give it a try in your Flutter projects!

#flutter #mediquery