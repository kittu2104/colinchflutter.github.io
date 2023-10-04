---
layout: post
title: "Drawing with generative algorithms in Flutter"
description: " "
date: 2023-10-04
tags: [generativealgorithms]
comments: true
share: true
---

Flutter is a popular cross-platform framework that allows developers to build beautiful and interactive user interfaces. While Flutter provides various tools for creating stunning designs, it can also be used for more creative purposes, such as generating visually appealing artwork using generative algorithms.

Generative algorithms use mathematical equations and randomization to create unique and aesthetically interesting patterns, shapes, and colors. In this blog post, we will explore how to leverage the power of generative algorithms to create stunning artwork in Flutter.

## Getting Started with Generative Algorithms in Flutter

To get started, let's create a new Flutter project and add the necessary dependencies. Open your favorite IDE and create a new Flutter project. Then, add the following dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  random_color: ^1.0.6
```

The `random_color` package will help us generate random colors for our artwork.

## Generating Random Colors

To create visually appealing artwork, we'll need to generate random colors. Add the following code snippet to your main.dart file:

```dart
import 'package:flutter/material.dart';
import 'package:random_color/random_color.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Generative Art',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Generative Art'),
        ),
        body: Center(
          child: Container(
            color: RandomColor().randomColor(),
          ),
        ),
      ),
    );
  }
}
```

In this code snippet, we import the `random_color` package and generate a random color using the `RandomColor().randomColor()` method. We set the color of the container widget to the generated random color.

## Creating Random Shapes

To create random shapes, we can leverage Flutter's custom painting capabilities. Add the following code snippet to your main.dart file:

```dart
import 'dart:math';

import 'package:flutter/material.dart';
import 'package:random_color/random_color.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Generative Art',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Generative Art'),
        ),
        body: CustomPaint(
          painter: ShapePainter(),
        ),
      ),
    );
  }
}

class ShapePainter extends CustomPainter {
  final random = Random();

  @override
  void paint(Canvas canvas, Size size) {
    final color = RandomColor().randomColor();
    final shapeType = random.nextInt(3);

    Paint paint = Paint()..color = color..strokeWidth = 2;

    switch (shapeType) {
      case 0:
        drawRectangle(canvas, paint, size);
        break;
      case 1:
        drawCircle(canvas, paint, size);
        break;
      case 2:
        drawTriangle(canvas, paint, size);
        break;
    }
  }

  void drawRectangle(Canvas canvas, Paint paint, Size size) {
    final rect = Rect.fromLTWH(random.nextDouble() * size.width,
        random.nextDouble() * size.height, 100, 100);
    canvas.drawRect(rect, paint);
  }

  void drawCircle(Canvas canvas, Paint paint, Size size) {
    final center = Offset(random.nextDouble() * size.width,
        random.nextDouble() * size.height);
    canvas.drawCircle(center, 50, paint);
  }

  void drawTriangle(Canvas canvas, Paint paint, Size size) {
    final path = Path();
    final startPoint = Offset(random.nextDouble() * size.width,
        random.nextDouble() * size.height);
    final endPoint1 = Offset(random.nextDouble() * size.width,
        random.nextDouble() * size.height);
    final endPoint2 = Offset(random.nextDouble() * size.width,
        random.nextDouble() * size.height);

    path.moveTo(startPoint.dx, startPoint.dy);
    path.lineTo(endPoint1.dx, endPoint1.dy);
    path.lineTo(endPoint2.dx, endPoint2.dy);
    path.lineTo(startPoint.dx, startPoint.dy);

    canvas.drawPath(path, paint);
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) {
    return true;
  }
}
```

In this code snippet, we create a `CustomPainter` class called `ShapePainter` that generates random shapes using the `Random` class from the `dart:math` package. We generate a random shape type and use the corresponding method to draw the shape on the canvas.

## Conclusion

In this blog post, we've explored how to use generative algorithms in Flutter to create unique and visually stunning artwork. We started by generating random colors and then moved on to creating random shapes using custom painting. Feel free to experiment and modify the code to further enhance your generative art creations using Flutter.

With the power of Flutter and generative algorithms, the possibilities for creating beautiful and interactive artwork are endless. So go ahead and let your creativity flow!

#flutter #generativealgorithms #ui #art