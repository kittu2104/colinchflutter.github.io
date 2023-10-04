---
layout: post
title: "Advanced drawings in Flutter using Bezier curves"
description: " "
date: 2023-10-04
tags: [BezierCurves]
comments: true
share: true
---

## Introduction
In Flutter, the `CustomPaint` widget allows us to create custom drawings using the `Canvas` API. Bezier curves are a powerful tool for drawing smooth and complex shapes. In this tutorial, we'll explore how to create advanced drawings in Flutter using Bezier curves.

## Prerequisites
Make sure you have Flutter and Dart installed on your machine. You can follow the official Flutter installation guide to get started.

## Getting Started
Create a new Flutter project and open the `main.dart` file. To draw using Bezier curves, we'll use the `drawBezier` method provided by the `CustomPainter` class. This method takes an instance of `Path` that defines the points and curves to draw.

Let's start by creating a simple example that draws a curved line.

```dart
import 'package:flutter/material.dart';

class BezierPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final path = Path();
    path.moveTo(50, 50);
    path.quadraticBezierTo(150, 100, 250, 50);

    final paint = Paint()
      ..color = Colors.blue
      ..style = PaintingStyle.stroke
      ..strokeWidth = 2;

    canvas.drawPath(path, paint);
  }

  @override
  bool shouldRepaint(BezierPainter oldDelegate) => false;
}

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      body: CustomPaint(painter: BezierPainter()),
    ),
  ));
}
```

In the above code, we define a `BezierPainter` class that extends `CustomPainter`. The `paint` method is responsible for drawing on the canvas. Here, we create a `Path` and use `quadraticBezierTo` to draw a curved line. We set the color, style, and width of the paint brush using the `Paint` class. The canvas draws the path using the paint brush.

To showcase the custom painting, we wrap the `CustomPaint` widget inside a `Scaffold` and `MaterialApp`. The `CustomPaint` widget takes an instance of `BezierPainter` as the `painter` property.

## Creating Complex Shapes
Bezier curves enable us to create more complex shapes. We can use multiple `cubicBezierTo` or `quadraticBezierTo` commands to draw curves with different control points. Additionally, we can use `lineTo` to draw straight lines.

Consider the following example that showcases a custom drawing of a heart shape:

```dart
class HeartPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final path = Path();
    path.moveTo(size.width / 2, size.height / 4);

    path.cubicTo(
      size.width * 0.7,
      size.height * 0.1,
      size.width * 0.9,
      size.height * 0.5,
      size.width / 2,
      size.height * 0.8,
    );

    path.cubicTo(
      size.width * 0.1,
      size.height * 0.5,
      size.width * 0.3,
      size.height * 0.1,
      size.width / 2,
      size.height / 4,
    );

    final paint = Paint()
      ..color = Colors.red
      ..style = PaintingStyle.fill;

    canvas.drawPath(path, paint);
  }

  @override
  bool shouldRepaint(HeartPainter oldDelegate) => false;
}

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      body: CustomPaint(painter: HeartPainter()),
    ),
  ));
}
```

In this code, we define a `HeartPainter` class that draws the heart shape using Bezier curves. We use `cubicTo` commands to define the control points for each curve. Finally, we set the color to red and the style to `PaintingStyle.fill` to fill the shape.

## Conclusion
Flutter provides a powerful `CustomPaint` widget that allows us to create advanced drawings using Bezier curves. These curves give us the flexibility to create smooth, complex shapes. By combining different types of Bezier commands, such as `quadraticBezierTo` and `cubicBezierTo`, we can draw various curves and lines to create stunning graphics in Flutter.

#flutter #BezierCurves