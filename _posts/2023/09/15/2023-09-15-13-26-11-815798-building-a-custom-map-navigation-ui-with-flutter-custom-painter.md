---
layout: post
title: "Building a custom map navigation UI with Flutter Custom Painter"
description: " "
date: 2023-09-15
tags: [flutter, flutterdevelopment]
comments: true
share: true
---

Navigation is an essential aspect of any map-based application. Flutter provides various widgets and tools to create beautiful and interactive user interfaces. In this tutorial, we will explore how to build a custom map navigation UI using the powerful Flutter Custom Painter.

## Understanding Flutter Custom Painter

The `CustomPaint` widget in Flutter allows us to create custom user interfaces by painting on a canvas. It provides a `CustomPainter` class that we can extend to define our own custom painting logic.

## Getting Started

To get started, create a new Flutter project and import the necessary packages. In the `pubspec.yaml` file, add the following dependencies:

```dart
dependencies:
  flutter:
    sdk: flutter
  vector_math: ^2.1.0
```

## Creating the Map Navigation UI

First, let's create a new Dart file called `map_navigation_ui.dart`. In this file, we will define a custom class called `MapNavigationUI` that extends `CustomPainter`. This class will handle the painting logic for our map navigation UI.

```dart
import 'package:flutter/material.dart';

class MapNavigationUI extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // Custom painting logic goes here
  }

  @override
  bool shouldRepaint(MapNavigationUI oldDelegate) {
    return false;
  }
}
```

Inside the `MapNavigationUI` class, we need to override two methods:

1. `paint`: This method is responsible for painting on the canvas. We will implement our custom painting logic here.
2. `shouldRepaint`: This method determines whether the `CustomPainter` should repaint when the delegate changes. In this case, we don't need to repaint, so we will return `false`.

## Implementing the Custom Painting Logic

Now, let's implement the custom painting logic for our map navigation UI. In the `paint` method, we will use various `drawPath`, `drawCircle`, and other canvas operations to draw the UI elements such as the map, user location marker, and navigation route.

```dart
import 'package:flutter/material.dart';
import 'package:vector_math/vector_math.dart' as vector;

class MapNavigationUI extends CustomPainter {
  final double userLocationX;
  final double userLocationY;
  final double destinationX;
  final double destinationY;

  MapNavigationUI({
    required this.userLocationX,
    required this.userLocationY,
    required this.destinationX,
    required this.destinationY,
  });

  @override
  void paint(Canvas canvas, Size size) {
    // Draw map
    final mapPath = Path();
    // ...
    canvas.drawPath(mapPath, Paint()..color = Colors.blue);

    // Draw user location marker
    final userLocation = Offset(userLocationX, userLocationY);
    canvas.drawCircle(userLocation, 10, Paint()..color = Colors.red);

    // Draw navigation route
    final routePath = Path();
    // ...
    canvas.drawPath(routePath, Paint()..color = Colors.green);
  }

  @override
  bool shouldRepaint(MapNavigationUI oldDelegate) {
    return false;
  }
}
```

In the code snippet above, we added four properties to the `MapNavigationUI` class: `userLocationX`, `userLocationY`, `destinationX`, and `destinationY`. These properties represent the coordinates of the user's location and the destination on the map.

We then implemented the painting logic inside the `paint` method. We created a `Path` object to represent the map, user location marker, and navigation route. Finally, we used the `canvas.drawPath` and `canvas.drawCircle` methods to draw these elements on the canvas.

## Using the Map Navigation UI

To use our custom map navigation UI, we need to integrate it with a Flutter widget. We will create a new widget called `MapNavigationScreen` and wrap it with the `CustomPaint` widget.

```dart
import 'package:flutter/material.dart';

class MapNavigationScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Map Navigation'),
      ),
      body: CustomPaint(
        painter: MapNavigationUI(
          userLocationX: 100,
          userLocationY: 200,
          destinationX: 300,
          destinationY: 400,
        ),
      ),
    );
  }
}
```

In the `MapNavigationScreen` widget, we used the `CustomPaint` widget and assigned our `MapNavigationUI` class as the `painter`. We provided dummy coordinates for the user's location and the destination.

## Conclusion

In this tutorial, we explored how to build a custom map navigation UI using Flutter Custom Painter. By extending the `CustomPainter` class, we were able to define our own custom painting logic and create an interactive map navigation UI.

Remember to leverage the power of Flutter Custom Painter to enhance the user experience and create visually appealing map-based applications.

#flutter #flutterdevelopment