---
layout: post
title: "Drawing with symmetry in Flutter"
description: " "
date: 2023-10-04
tags: [setting]
comments: true
share: true
---

In this article, we will explore how to create beautiful and symmetrical drawings in Flutter using the `CustomPaint` widget and the concept of symmetry. Symmetry is a powerful design principle that can add elegance and balance to your UI. By leveraging Flutter's painting system, we can easily achieve stunning symmetrical effects in our applications.

## Table of Contents
1. [Introduction](#introduction)
2. [Setting Up the Project](#setting-up-the-project)
3. [Creating the CustomPainter](#creating-the-custompainter)
4. [Implementing Symmetry](#implementing-symmetry)
5. [Symmetry Types](#symmetry-types)
6. [Final Thoughts](#final-thoughts)

## Introduction
Symmetry is the property of an object that allows it to be divided into two or more identical parts. It plays a significant role in art and design, contributing to visual balance and harmony. Flutter, an expressive UI toolkit, gives us the tools to create visually appealing and symmetrical drawings effortlessly.

## Setting Up the Project
To get started, create a new Flutter project or open an existing one. Open the `pubspec.yaml` file and add the following dependency:

```yaml
dependencies:
  flutter:
    sdk: flutter
  vector_math: ^2.1.0
```
After saving the `pubspec.yaml` file, run `flutter pub get` to download the added dependency.

## Creating the CustomPainter
Next, create a new Dart file, such as `symmetry_painter.dart`, and define the `SymmetryPainter` class.

```dart
import 'dart:ui';
import 'package:flutter/material.dart';

class SymmetryPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // Drawing logic goes here
  }

  @override
  bool shouldRepaint(SymmetryPainter oldDelegate) {
    return false; // Only repaint when necessary
  }
}
```

In the `paint` method, we will implement the drawing logic, and in the `shouldRepaint` method, we can control if the painter should repaint itself. For this implementation, we can assume that the painter doesn't need to be repainted unless we explicitly specify it.

## Implementing Symmetry
To add symmetry to our drawing, we need to transform the canvas accordingly. Flutter provides a `Matrix4` class from the `vector_math` package, which allows us to apply transformations to the canvas. Let's update the `paint` method to include symmetry:

```dart
void paint(Canvas canvas, Size size) {
  // Set up the transformation matrix
  final center = size.center(Offset.zero);
  final matrix = Matrix4.identity();
  matrix.translate(center.dx, center.dy);
  canvas.transform(matrix.storage);

  // Drawing logic with symmetry goes here
}
```

In the above code, we are first obtaining the center position of the canvas and creating a transformation matrix. Then, we are translating the matrix to the center position to ensure that the drawing starts from the center of the canvas.

## Symmetry Types
There are various types of symmetry, including vertical, horizontal, diagonal, radial, and more. Let's explore a simple example using vertical symmetry.

```dart
void paint(Canvas canvas, Size size) {
  // Set up the transformation matrix

  // Draw the first half of the shape
  Path path = Path();
  path.moveTo(0, 0);
  path.lineTo(0, size.height);
  path.lineTo(size.width / 2, size.height / 2);
  path.close();

  canvas.drawPath(path, Paint());

  // Apply symmetry by reflecting the canvas
  final reflectedMatrix = Matrix4.identity();
  reflectedMatrix.scale(-1.0, 1.0);
  canvas.transform(reflectedMatrix.storage);

  // Draw the reflected half of the shape
  canvas.drawPath(path, Paint());
}
```

In this example, we create a simple triangle that is split in half vertically. We draw the first half of the shape and then apply symmetry by reflecting the canvas along the vertical axis. Finally, we draw the reflected half of the shape.

## Final Thoughts
Symmetry is an excellent technique to achieve balance and harmony in your designs. Flutter provides a powerful painting system that allows you to easily implement symmetry in your applications. Experiment with different symmetry types and explore creative ways to incorporate symmetry into your UI.

Remember to save your work regularly and test your code as you go. Happy coding!

#flutter #symmetry