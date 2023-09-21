---
layout: post
title: "Creating a custom shape progress bar with percentage using CustomClipper in Flutter"
description: " "
date: 2023-09-21
tags: []
comments: true
share: true
---

![](https://example.com/progress-bar.png)

In this tutorial, we will explore how to create a custom shape progress bar with the percentage indicator using the `CustomClipper` class in Flutter. We will be able to easily customize the shape and style of the progress bar according to our needs.

## Getting Started

To get started, make sure you have Flutter installed on your system. If you don't have Flutter installed, you can follow the official [Flutter installation guide](https://flutter.dev/docs/get-started/install).

## Creating the CustomClipper Class

First, we need to create a custom class that extends the `CustomClipper` class. This class will define the shape of our progress bar.

```dart
import 'dart:math';
import 'package:flutter/material.dart';

class ProgressShapeClipper extends CustomClipper<Path> {
  @override
  Path getClip(Size size) {
    final path = Path();
    path.moveTo(0, size.height / 2);
    path.lineTo(size.width, size.height / 2);
    path.lineTo(size.width, size.height);
    path.lineTo(0, size.height);
    path.close();
    return path;
  }

  @override
  bool shouldReclip(CustomClipper<Path> oldClipper) {
    return true;
  }
}
```

In the `getClip` method, we define the shape of our progress bar using a `Path` object. In this example, we are creating a simple rectangle shape, but you can modify this method to create any custom shape you desire.

The `path.close()` method closes the path, completing the shape. Finally, the `shouldReclip` method determines whether to recalculate the clipping path if the size of the widget changes.

## Implementing the Custom Shape Progress Bar

Now, let's implement our custom shape progress bar widget using the `ProgressShapeClipper` class.

```dart
class CustomShapeProgressBar extends StatelessWidget {
  final double width;
  final double height;
  final int percentage;
  final Color backgroundColor;
  final Color progressColor;

  CustomShapeProgressBar({
    required this.width,
    required this.height,
    required this.percentage,
    required this.backgroundColor,
    required this.progressColor,
  });

  @override
  Widget build(BuildContext context) {
    return ClipPath(
      clipper: ProgressShapeClipper(),
      child: Container(
        width: width,
        height: height,
        color: backgroundColor,
        child: Stack(
          children: [
            Container(
              height: height,
              width: width * percentage / 100,
              color: progressColor,
            ),
            Center(
              child: Text(
                '$percentage%',
                style: TextStyle(
                  color: Colors.white,
                  fontWeight: FontWeight.bold,
                ),
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

In the above code, we are using the `ClipPath` widget to apply our custom shape clipper. Inside the `ClipPath`, we have a `Container` that acts as the background for the progress bar.

We use a `Stack` widget to stack the progress bar and the percentage text widget on top of the background. The width of the progress bar is calculated based on the provided `percentage` value.

## Using the Custom Shape Progress Bar

To use our custom shape progress bar widget, simply create an instance of `CustomShapeProgressBar` and provide the required parameters.

```dart
CustomShapeProgressBar(
  width: 300,
  height: 40,
  percentage: 75,
  backgroundColor: Colors.grey,
  progressColor: Colors.blue,
)
```

Make sure to adjust the `width`, `height`, `percentage`, and color values according to your needs.

## Conclusion

In this tutorial, we learned how to create a custom shape progress bar with a percentage indicator using the `CustomClipper` class in Flutter. We covered creating a custom shape clipper class and implementing a custom shape progress bar widget based on it.

By creating custom shapes, you can easily customize the progress bar in your Flutter application to match your design requirements.