---
layout: post
title: "Creating a neon light effect in Flutter drawing"
description: " "
date: 2023-10-04
tags: [ custom]
comments: true
share: true
---

In this tutorial, we will learn how to create a neon light effect in Flutter drawing using the built-in Canvas API. The neon light effect adds a vibrant and glowing appearance to our drawn shapes or text. Let's get started!

## Table of Contents
1. [Setting up the Project](#setup)
2. [Creating a Custom Painter](#custom-painter)
3. [Drawing Shapes with Neon Light Effect](#drawing)
4. [Applying Neon Effect to Text](#text-effect)
5. [Conclusion](#conclusion)

## 1. Setting up the Project<a name="setup"></a>

First, let's set up a new Flutter project by following these steps:

```bash
# Create a new Flutter project
flutter create neon_light

# Change directory to the project
cd neon_light

# Open the project in your preferred text editor or IDE
```

## 2. Creating a Custom Painter<a name="custom-painter"></a>

Next, we need to create a custom painter class that will handle our drawing and implement the `CustomPainter` interface. This class will be responsible for painting our neon light effect on the canvas.

```dart
import 'package:flutter/material.dart';

class NeonPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // Implement the drawing logic here
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    return false;
  }
}
```

## 3. Drawing Shapes with Neon Light Effect<a name="drawing"></a>

To draw shapes with a neon light effect, we will make use of the `drawPath` method provided by the `Canvas` class. We will create a `Path` object representing the shape we want to draw and then pass it to the `drawPath` method.

Here's an example of drawing a rectangle shape with a neon light effect:

```dart
Path rectPath = Path()
  ..moveTo(50, 50)
  ..lineTo(150, 50)
  ..lineTo(150, 150)
  ..lineTo(50, 150)
  ..close();

Paint neonPaint = Paint()
  ..color = Colors.blue
  ..style = PaintingStyle.stroke
  ..strokeWidth = 4;

canvas.drawPath(rectPath, neonPaint);
```

You can experiment with different shapes and colors to achieve your desired neon light effect. Remember to adjust the `color` and `strokeWidth` properties of the `Paint` object to customize the effect.

## 4. Applying Neon Effect to Text<a name="text-effect"></a>

To apply the neon light effect to text, we can make use of the `drawText` method provided by the `Canvas` class. We will create a `TextSpan` object with the desired text and style, and then pass it to the `drawText` method.

Here's an example of applying a neon light effect to text:

```dart
TextSpan textSpan = TextSpan(
  text: "Neon Light",
  style: TextStyle(
    color: Colors.blue,
    fontSize: 24,
    shadows: [
      Shadow(
        blurRadius: 8,
        color: Colors.blue,
        offset: Offset(0, 0),
      ),
    ],
  ),
);

TextPainter textPainter = TextPainter(
  text: textSpan,
  textDirection: TextDirection.ltr,
);

textPainter.layout();

textPainter.paint(canvas, Offset(50, 50));
```

Adjust the `color` and `blurRadius` properties of the `Shadow` object to customize the neon light effect on the text.

## 5. Conclusion<a name="conclusion"></a>

In this tutorial, we have learned how to create a neon light effect in Flutter drawing using the Canvas API. We explored drawing shapes with a neon light effect and applying the effect to text. Experiment with different shapes, colors, and texts to achieve stunning neon light effects in your Flutter applications.

Don't forget to share your creations with us! Happy coding! 🚀

**#Flutter #NeonLightEffect**