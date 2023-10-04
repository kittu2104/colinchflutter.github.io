---
layout: post
title: "Creating a spirograph in Flutter drawing"
description: " "
date: 2023-10-04
tags: [Flutter, Drawing]
comments: true
share: true
---

In this tutorial, we will explore how to create a spirograph using Flutter drawing capabilities. A spirograph is a geometric drawing toy that produces mathematical curves known as hypotrochoids and epitrochoids. With Flutter, we can easily create complex drawings and animations to recreate this classic toy.

## Table of Contents
1. Introduction
2. Setting up the Flutter Project
3. Creating the Spirograph Widget
4. Drawing Hypotrochoids and Epitrochoids
5. Customizing the Spirograph
6. Conclusion

## 1. Introduction
Spirographs are fascinating geometric patterns that can be created using basic principles of circles rolling inside each other. By controlling the radii and the distance between the circles, we can generate intricate and beautiful designs.

## 2. Setting up the Flutter Project
To get started, make sure you have Flutter installed on your system. Create a new Flutter project by running the following commands in your terminal:

```
flutter create spirograph_app
cd spirograph_app
```

You can use any IDE or code editor of your choice to work on this project.

## 3. Creating the Spirograph Widget
In the `lib` folder of your Flutter project, create a new file called `spirograph_widget.dart`. Inside this file, we will define our custom SpirographWidget class.

```dart
import 'package:flutter/material.dart';

class SpirographWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CustomPaint(
      painter: SpirographPainter(), // Create a custom painter for drawing
    );
  }
}
```

## 4. Drawing Hypotrochoids and Epitrochoids
Now, let's create the custom painter class, `SpirographPainter`, that will handle the drawing of the spirograph.

```dart
import 'dart:math';
import 'package:flutter/material.dart';

class SpirographPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // Define your spirograph parameters
    double R = 80; // Radius of the base circle
    double r = 30; // Radius of the rolling circle
    double d = 50; // Distance between the centers of the two circles

    // Calculate the number of iterations for a complete spirograph
    double gcd = _calculateGCD(R, r);
    double numIterations = (2 * pi * r) / gcd;

    // Set stroke properties
    Paint paint = Paint()
      ..color = Colors.blue
      ..strokeWidth = 2
      ..style = PaintingStyle.stroke;

    // Initialize the starting point
    Path path = Path();
    double startX = R - r + d;
    double startY = 0;
    path.moveTo(startX, startY);

    // Generate the spirograph path
    for (double t = 0; t <= numIterations; t += 0.01) {
      double x = (R - r) * cos(t) + d * cos(((R - r) / r) * t);
      double y = (R - r) * sin(t) - d * sin(((R - r) / r) * t);
      path.lineTo(x, y);
    }

    // Draw the spirograph on the canvas
    canvas.drawPath(path, paint);
  }

  double _calculateGCD(double a, double b) {
    if (b == 0) {
      return a;
    }
    return _calculateGCD(b, a % b);
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    return false;
  }
}
```

## 5. Customizing the Spirograph
You can customize the spirograph by modifying the values of `R`, `r`, and `d` in the `SpirographPainter` class. Experiment with different values to create unique and interesting patterns.

To display the spirograph widget, update the `main.dart` file in the `lib` folder:

```dart
import 'package:flutter/material.dart';
import 'package:spirograph_app/spirograph_widget.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Spirograph App',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Spirograph'),
        ),
        body: Center(
          child: SpirographWidget(),
        ),
      ),
    );
  }
}
```

## 6. Conclusion
Congratulations! You have successfully created a spirograph in Flutter drawing. Experiment with different parameters and have fun creating unique spirograph patterns. Flutter's drawing capabilities allow you to explore various geometric shapes and designs. Feel free to further enhance the spirograph or explore other possibilities with Flutter drawing. Happy coding!

Don't forget to check out our #Flutter and #Drawing hashtags for more Flutter and drawing-related content.