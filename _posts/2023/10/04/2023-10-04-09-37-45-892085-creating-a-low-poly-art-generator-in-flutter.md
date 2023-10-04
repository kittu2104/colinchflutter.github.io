---
layout: post
title: "Creating a low-poly art generator in Flutter"
description: " "
date: 2023-10-04
tags: [introduction), getting]
comments: true
share: true
---

Flutter is a versatile framework that allows developers to create beautiful and interactive user interfaces for mobile, web, and desktop applications. In this tutorial, we will explore how to create a low-poly art generator using Flutter. 

## Table of Contents
- [Introduction](#introduction)
- [Getting Started](#getting-started)
- [Creating a Polygon](#creating-a-polygon)
- [Generating Low-Poly Art](#generating-low-poly-art)
- [Conclusion](#conclusion)

## Introduction <a name="introduction"></a>

Low-poly art refers to a style of digital art where images are composed of numerous geometric shapes, usually triangles, to create a simplified and abstract representation of an object or scene. By generating low-poly art programmatically, we can create unique and visually appealing images.

## Getting Started <a name="getting-started"></a>

To get started, make sure you have Flutter installed and set up on your development environment. If you haven't, you can refer to the official Flutter documentation for installation instructions.

Once you have Flutter set up, create a new Flutter project using the following command:

```
flutter create low_poly_art_generator
```

Next, navigate into the project directory and open the `lib/main.dart` file. This is where we will write our code.

First, we need to import the necessary packages:

```dart
import 'dart:math';
import 'package:flutter/material.dart';
```

Next, we can create a new `LowPolyArtGenerator` widget:

```dart
class LowPolyArtGenerator extends StatefulWidget {
  @override
  _LowPolyArtGeneratorState createState() => _LowPolyArtGeneratorState();
}

class _LowPolyArtGeneratorState extends State<LowPolyArtGenerator> {
  @override
  Widget build(BuildContext context) {
    // TODO: Implement widget UI
  }
}
```

Now, we can move on to creating the polygon shape.

## Creating a Polygon <a name="creating-a-polygon"></a>

In this example, we will create a simple equilateral triangle as our polygon shape.

To create the polygon, we can define a new `CustomPainter`:

```dart
class PolygonPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // TODO: Implement polygon painting logic
  }

  @override
  bool shouldRepaint(PolygonPainter oldDelegate) => false;
}
```

Inside the `paint` method, we can use the `Canvas` object to draw the polygon shape. Using the `Path` class, we can define the vertices of the triangle:

```dart
Path path = Path();
path.moveTo(size.width / 2, 0);  // Top vertex
path.lineTo(size.width, size.height);  // Bottom right vertex
path.lineTo(0, size.height);  // Bottom left vertex
path.close();  // Connect back to the top vertex
```

Finally, we can use a `Paint` object to define the fill and stroke properties of the polygon:

```dart
Paint paint = Paint()
  ..color = Colors.blue // Triangle fill color
  ..style = PaintingStyle.fill;
```

## Generating Low-Poly Art <a name="generating-low-poly-art"></a>

Now that we have our polygon shape, we can generate a low-poly art image by repeating and randomly positioning the triangles on a canvas.

Inside the `LowPolyArtGenerator` widget's `build` method, we can utilize a `GridView` to display a grid of triangles:

```dart
GridView.count(
  crossAxisCount: 10,  // Number of columns in the grid
  children: List.generate(100, (index) => CustomPaint(painter: PolygonPainter())),
),
```

The `crossAxisCount` property determines the number of columns in the grid, and the `children` property generates the desired number of triangles using the `PolygonPainter` as the `CustomPaint` widget's `painter`.

## Conclusion <a name="conclusion"></a>

In this tutorial, we learned how to create a low-poly art generator in Flutter. We explored the basics of drawing a polygon shape using `CustomPainter` and generating a low-poly art grid using `GridView`. With these techniques, you can further enhance the generator by adding interactivity or customizing the shapes and colors.

Remember to experiment and have fun with the low-poly art generator to create unique and visually appealing artwork in your Flutter applications!

#flutter #lowpolyart #fluttertutorial