---
layout: post
title: "Using SkiaShadersMask for creating interactive maps in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

In this tutorial, we will explore how to create interactive maps in Flutter using SkiaShadersMask. Skia is a 2D graphics library developed by Google, and Flutter provides a Skia binding to enable the use of Skia shaders in Flutter applications. SkiaShadersMask allows us to apply masks to widgets, which is great for creating interactive maps where specific regions can be selected or highlighted.

## Table of Contents
1. [Setting up the project](#setting-up-the-project)
2. [Creating a basic map](#creating-a-basic-map)
3. [Adding interaction with SkiaShadersMask](#adding-interaction-with-skiashadersmask)
4. [Conclusion](#conclusion)

## Setting up the project<a name="setting-up-the-project"></a>

To get started, create a new Flutter project in your desired IDE. Open the pubspec.yaml file and add the following dependency:

```dart
dependencies:
  flutter:
    sdk: flutter
  flutter_skia_shaders: ^1.1.0
```

Save the file and run `flutter pub get` to install the dependency.

## Creating a basic map<a name="creating-a-basic-map"></a>

Next, create a new file called `map_screen.dart` and add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_skia_shaders/flutter_skia_shaders.dart';

class MapScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Interactive Map'),
      ),
      body: Center(
        child: Container(
          width: 300,
          height: 300,
          child: CustomPaint(
            painter: MapPainter(),
          ),
        ),
      ),
    );
  }
}

class MapPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final paint = Paint()..color = Colors.blue;
    canvas.drawRect(Rect.fromLTWH(0, 0, size.width, size.height), paint);
  }

  @override
  bool shouldRepaint(MapPainter oldDelegate) => false;
}
```

In this code, we create a basic map screen with a `CustomPaint` widget that uses the `MapPainter` custom painter. The `MapPainter` class overrides the `paint` method to draw a blue rectangle on the canvas.

## Adding interaction with SkiaShadersMask<a name="adding-interaction-with-skiashadersmask"></a>

To make the map interactive, we can use the `SkiaShadersMask` widget provided by the `flutter_skia_shaders` package. Modify the `MapScreen` class as follows:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_skia_shaders/flutter_skia_shaders.dart';

class MapScreen extends StatefulWidget {
  @override
  _MapScreenState createState() => _MapScreenState();
}

class _MapScreenState extends State<MapScreen> {
  List<Offset> selectedPoints = [];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Interactive Map'),
      ),
      body: GestureDetector(
        onTapUp: (TapUpDetails details) {
          setState(() {
            selectedPoints.add(details.localPosition);
          });
        },
        child: Center(
          child: Container(
            width: 300,
            height: 300,
            child: SkiaShadersMask(
              shaderMask: (Size size) => _createShaderMask(size),
              child: CustomPaint(
                painter: MapPainter(selectedPoints),
              ),
            ),
          ),
        ),
      ),
    );
  }

  ShaderMask _createShaderMask(Size size) {
    if (selectedPoints.isEmpty) {
      return null;
    } else {
      Path path = Path();
      path.addPolygon(selected