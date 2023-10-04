---
layout: post
title: "Drawing circles in Flutter"
description: " "
date: 2023-10-04
tags: [drawing, circles]
comments: true
share: true
---
Flutter is a powerful framework for building cross-platform applications, and it includes a wide range of built-in widgets and functionality. In this blog post, we'll explore how to draw circles in Flutter using various approaches.

## Using the `CustomPaint` widget
The `CustomPaint` widget in Flutter allows you to create custom drawings by providing a `CustomPainter` object. To draw a circle, you can create a custom painter and implement the `paint` method.

```dart
import 'package:flutter/material.dart';

class CirclePainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final paint = Paint()
      ..color = Colors.red
      ..style = PaintingStyle.fill;

    final center = Offset(size.width / 2, size.height / 2);
    final radius = size.width / 4;

    canvas.drawCircle(center, radius, paint);
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) => false;
}

class MyCircleWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      width: 200,
      height: 200,
      child: CustomPaint(
        painter: CirclePainter(),
      ),
    );
  }
}

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      appBar: AppBar(
        title: Text('Circle Example'),
      ),
      body: Center(
        child: MyCircleWidget(),
      ),
    ),
  ));
}
```

In the code snippet above, we create a custom painter `CirclePainter` that implements the `paint` method to draw a circle. We then use the `CustomPaint` widget inside a `Container` widget to define the dimensions of our circle. Finally, we wrap it in a `Center` widget to center the circle on the screen.

## Using the `Container` widget and `ShapeDecoration`
Another approach to drawing circles in Flutter is to use the `Container` widget along with the `ShapeDecoration` class. With this approach, we can define the shape of the container as a circle.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      appBar: AppBar(
        title: Text('Circle Example'),
      ),
      body: Center(
        child: Container(
          width: 200,
          height: 200,
          decoration: ShapeDecoration(
            shape: CircleBorder(),
            color: Colors.red,
          ),
        ),
      ),
    ),
  ));
}
```

In the code snippet above, we define a `Container` widget with a specified width and height, and set its decoration to a `ShapeDecoration` with a `CircleBorder` shape. We also set the color of the circle to red. The `CircleBorder` shape creates a circle based on the dimensions of the `Container`.

## Conclusion
Flutter provides multiple ways to draw circles in your applications. Whether you choose to use the `CustomPaint` widget or the `Container` widget with `ShapeDecoration`, you can easily create visually appealing circle shapes. Experiment with different colors, sizes, and positioning to bring your designs to life!

#flutter #drawing #circles