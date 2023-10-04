---
layout: post
title: "Creating shapes using the Flutter Canvas"
description: " "
date: 2023-10-04
tags: [getting, drawing]
comments: true
share: true
---

Flutter is a powerful framework for building beautiful user interfaces. One of the key features of Flutter is the **Canvas** class, which allows us to draw shapes and render graphics on the screen. In this blog post, we will explore how to create different shapes using the Flutter Canvas.

## Table of Contents

- [Getting Started](#getting-started)
- [Drawing a Rectangle](#drawing-a-rectangle)
- [Creating a Circle](#creating-a-circle)
- [Drawing a Triangle](#drawing-a-triangle)
- [Conclusion](#conclusion)

## Getting Started

To get started, you first need to create a new Flutter project and import the `dart:ui` library. The `dart:ui` library provides the `Canvas` class, which we will use to draw shapes on the screen.

```dart
import 'package:flutter/material.dart';
import 'dart:ui' as ui;

class MyCanvasWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CustomPaint(
      painter: MyPainter(),
    );
  }
}

class MyPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // Your code here
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    return false;
  }
}
```

In the `MyPainter` class, we need to implement two methods: `paint` and `shouldRepaint`.

## Drawing a Rectangle

To draw a rectangle using the Flutter Canvas, we can use the `canvas.drawRect` method. This method takes in a `Rect` object, which specifies the dimensions and position of the rectangle.

```dart
Rect rect = Rect.fromLTWH(50, 50, 200, 100);
Paint paint = Paint()..color = Colors.blue;

canvas.drawRect(rect, paint);
```

## Creating a Circle

To create a circle, we can use the `canvas.drawCircle` method. This method takes in a `Offset` object, which specifies the center of the circle, and a radius value.

```dart
Offset center = Offset(150, 150);
double radius = 50;
Paint paint = Paint()..color = Colors.red;

canvas.drawCircle(center, radius, paint);
```

## Drawing a Triangle

Drawing a triangle requires a bit more effort. We need to use the `canvas.drawPath` method and define a `Path` object that represents the shape of the triangle.

```dart
Path path = Path();
path.moveTo(100, 100);
path.lineTo(200, 200);
path.lineTo(100, 200);
path.close();

Paint paint = Paint()..color = Colors.green;

canvas.drawPath(path, paint);
```

## Conclusion

In this blog post, we have learned how to create different shapes using the Flutter Canvas. Flutter offers a flexible and powerful way to draw graphics, and the Canvas class provides various methods to render shapes on the screen. Experiment with different shapes and colors to create stunning UI elements in your Flutter applications.

#flutter #canvas