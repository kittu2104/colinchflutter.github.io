---
layout: post
title: "How to create adaptive designs with `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [flutter, responsive]
comments: true
share: true
---

Creating adaptive designs is crucial in today's world of mobile devices with different screen sizes and orientations. Flutter provides a powerful tool called `MediaQuery` to help you create responsive layouts that automatically adapt to various device sizes. In this blog post, we will explore how to use `MediaQuery` to create adaptive designs in Flutter.

## What is MediaQuery?

`MediaQuery` is a Flutter class that provides information about the current device's screen size, orientation, and other properties. It gives you a way to access the device's constraints and adjust your UI layout accordingly. For example, you can use `MediaQuery` to determine the device's screen width and height and dynamically adjust the size and position of your UI elements.

## Using MediaQuery for adaptive designs

To use `MediaQuery` in your Flutter project, you can simply wrap your top-level widget or the widget that needs to adapt to the device's properties with a `MediaQuery` widget.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: MediaQuery(
        data: MediaQueryData(),
        child: Scaffold(
          appBar: AppBar(
            title: Text('Adaptive Design'),
          ),
          body: MyAdaptiveWidget(),
        ),
      ),
    );
  }
}

class MyAdaptiveWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Center(
      child: Container(
        width: MediaQuery.of(context).size.width * 0.8,
        height: MediaQuery.of(context).size.height * 0.5,
        color: Colors.blue,
        child: Text(
          'Adaptive Content',
          style: TextStyle(
            fontSize: 24.0,
            color: Colors.white,
          ),
        ),
      ),
    );
  }
}
```

In the above code snippet, we wrap the `Scaffold` widget with `MediaQuery` and pass an empty `MediaQueryData` object. This ensures that the `MediaQuery` widget inherits the device's constraints.

Inside the `MyAdaptiveWidget` build method, we use `MediaQuery.of(context)` to access the `MediaQueryData` object and extract the device's screen width and height. We then use this information to set the width and height of the `Container` widget accordingly.

As a result, the `Container` widget will have adaptive dimensions based on the device's screen size.

## Responsive layouts with MediaQuery

You can also use `MediaQuery` to create responsive layouts in Flutter. For example, you can use the `orientation` property of `MediaQueryData` to determine whether the device is in portrait or landscape mode and adjust your UI accordingly.

```dart
class MyResponsiveWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final Orientation orientation = MediaQuery.of(context).orientation;
    
    return orientation == Orientation.portrait
        ? Container(
            // Portrait mode layout
          )
        : Container(
            // Landscape mode layout
          );
  }
}
```

In the above example, we use the `orientation` property of `MediaQueryData` to determine whether the device is in portrait or landscape mode. Based on the orientation, we select and render the appropriate layout.

## Conclusion

Using `MediaQuery`, you can create adaptive designs and responsive layouts in Flutter that automatically adjust to the device's screen size, orientation, and other properties. By leveraging this powerful tool, you can ensure that your app looks great on various devices and provides an optimal user experience.

Try incorporating `MediaQuery` in your Flutter projects and start building adaptive designs today!

#flutter #responsive-design