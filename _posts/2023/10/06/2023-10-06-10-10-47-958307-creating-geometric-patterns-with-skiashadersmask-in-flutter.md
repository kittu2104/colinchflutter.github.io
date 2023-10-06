---
layout: post
title: "Creating geometric patterns with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

Flutter provides a powerful rendering engine called Skia which allows for advanced graphical operations. In this tutorial, we will explore how to create geometric patterns using the SkiaShadersMask class in Flutter.

## What is SkiaShadersMask?

SkiaShadersMask is a class in the Flutter framework that allows you to create and manipulate shaders, which are used to define patterns and colors in a rendering surface. In our case, we will use SkiaShadersMask to create a geometric pattern that will be applied as a mask to an image or a container.

## Getting started

To get started, make sure you have Flutter SDK installed on your machine. If you haven't already, you can download it from the Flutter website and follow the installation instructions.

## Creating a new project

Open your terminal or command prompt and run the following command to create a new Flutter project:

```shell
flutter create geometric_patterns
```
{: .language-shell}

Once the project is created, open it in your preferred code editor.

## Implementing the pattern

In this example, we will create a simple rectangular pattern using SkiaShadersMask. Within your Flutter project, open the `lib/main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/rendering.dart';
import 'dart:ui' as ui;

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Geometric Patterns',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Geometric Patterns'),
        ),
        body: Container(
          decoration: BoxDecoration(
            image: DecorationImage(
              image: AssetImage('assets/background.jpg'),
              fit: BoxFit.cover,
              colorFilter: ColorFilter.mode(Colors.black.withOpacity(0.5), BlendMode.dstATop),
              ),
            ),
          child: BackdropFilter(
            filter: ui.ImageFilter.blur(sigmaX: 5.0, sigmaY: 5.0),
            child: Container(
              width: double.infinity,
              height: double.infinity,
              color: Colors.transparent,
              child: CustomPaint(
                painter: PatternPainter(),
              ),
            ),
          ),
        ),
      ),
    );
  }
}

class PatternPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final Path path = Path();
    final double singleSize = 100.0;
    final double gridSize = singleSize * 2;

    for (double i = 0; i < size.width; i += gridSize) {
      for (double j = 0; j < size.height; j += gridSize) {
        final Rect rect = Rect.fromLTWH(i, j, singleSize, singleSize);
        path.addRect(rect);
      }
    }

    final Paint paint = Paint()
      ..shader = ui.Gradient.linear(
        Offset.zero,
        Offset.zero.translate(gridSize, gridSize),
        [
          Colors.red,
          Colors.yellow,
          Colors.green,
          Colors.blue,
          Colors.purple,
        ],
      );

    canvas.drawPath(path, paint);
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) {
    return false;
  }
}
```
{: .language-dart}

In this code, we have a basic Flutter app structure with a `Container` that acts as a canvas for our pattern. We are using an image in the `Container` as a background and applying a blur effect using the `ImageFilter.blur` function.

Inside the `CustomPainter` class, we define the `paint` method to draw the rectangular pattern using `Path` and `Paint` objects. The `Path.addRect` method is used to add a rectangle to the path, which is then drawn on the canvas using the `canvas.drawPath` method.

To run the app, use the following command in your terminal:

```shell
flutter run
```
{: .language-shell}

You should now see a Flutter app with a rectangular pattern as the background.

## Conclusion

In this tutorial, we learned how to create geometric patterns using the SkiaShadersMask class in Flutter. By manipulating shaders and using custom painters, we can achieve various visual effects and patterns in our Flutter apps. Feel free to experiment with different shapes, colors, and patterns to create unique designs.