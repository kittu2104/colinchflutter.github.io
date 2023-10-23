---
layout: post
title: "Handling different screen orientations in MaterialApp."
description: " "
date: 2023-10-23
tags: [tags, ScreenOrientation]
comments: true
share: true
---

One of the challenges in building a responsive user interface is handling different screen orientations. In this blog post, we will explore how to handle screen orientation changes in a `MaterialApp` widget in Flutter.

## Table of Contents
- [Introduction](#introduction)
- [Detecting Screen Orientation](#detecting-screen-orientation)
- [Handling Orientation Changes](#handling-orientation-changes)
- [Example Code](#example-code)
- [Conclusion](#conclusion)

## Introduction

By default, `MaterialApp` doesn't handle screen orientation changes automatically. When the screen rotates, the UI may not adjust accordingly, leading to a poor user experience. However, Flutter provides a way to detect screen orientation changes and update the UI accordingly.

## Detecting Screen Orientation

To detect screen orientation changes, we can use the `OrientationBuilder` widget. It allows us to rebuild parts of the UI based on the current screen orientation. The `OrientationBuilder` takes a builder function that provides the current orientation as a parameter.

## Handling Orientation Changes

To handle orientation changes, we can wrap the parts of the UI that need to be updated in response to a screen rotation inside the `OrientationBuilder` widget. Within the builder function, we can conditionally render different UI elements based on the current orientation.

For example, suppose we want to display a different layout for landscape and portrait modes. We can use the `MediaQuery` to get the current orientation and conditionally render different UI elements.

## Example Code

Here is an example of how to handle different screen orientations in a `MaterialApp`:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(home: MyApp()));
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Handling Screen Orientations"),
      ),
      body: OrientationBuilder(
        builder: (context, orientation) {
          return Container(
            child: Text(
              orientation == Orientation.portrait
                  ? "Portrait Mode"
                  : "Landscape Mode",
              style: TextStyle(fontSize: 24.0),
            ),
          );
        },
      ),
    );
  }
}
```

In the above code, we wrap the `Text` widget inside the `OrientationBuilder` and check the current orientation using the `Orientation` enum. We render different text based on the orientation.

## Conclusion

Handling different screen orientations is crucial for creating a user-friendly interface. By using the `OrientationBuilder` widget and conditionally rendering UI elements, we can ensure that our app adjusts gracefully to different screen orientations. Experiment with the provided code to see how you can customize your app based on orientation changes.

Remember, providing an optimal user experience across various screen sizes and orientations is an essential aspect of app development.

#tags: #Flutter #ScreenOrientation