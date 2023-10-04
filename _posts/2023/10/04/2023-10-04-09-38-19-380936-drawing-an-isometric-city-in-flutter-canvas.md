---
layout: post
title: "Drawing an isometric city in Flutter Canvas"
description: " "
date: 2023-10-04
tags: [Flutter, Canvas]
comments: true
share: true
---

In this tutorial, we will learn how to use the Flutter Canvas to draw an isometric city. Isometric drawing is a technique used to create 3D-like objects in a 2D space. We will use the Flutter framework's Canvas class to draw rectangles and paths to represent buildings, streets, and other elements of the city. Let's get started!

## Getting Started

To begin, create a new Flutter project and replace the contents of the `main.dart` file with the following code:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: CustomPaint(
          painter: CityPainter(),
        ),
      ),
    );
  }
}

class CityPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // TODO: Implement drawing logic
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) => false;
}
```

This code sets up a basic Flutter application with a CustomPainter that we will use to draw our city.

## Drawing the Buildings

To draw the buildings, we will create a `drawBuilding` method inside the `CityPainter` class. The method will take in a `Canvas` object, the `x` and `y` coordinates of the top-left corner of the building, and the building's width and height.

```dart
void drawBuilding(Canvas canvas, double x, double y, double width, double height) {
  final paint = Paint()..color = Colors.blue;

  final path = Path()
    ..moveTo(x, y)
    ..lineTo(x + width, y)
    ..lineTo(x + width, y + height)
    ..lineTo(x, y + height)
    ..close();

  canvas.drawPath(path, paint);
}
```

The `drawBuilding` method creates a `Paint` object with the desired color and defines a `Path` object that represents the outline of the building. We then use the `drawPath` method on the `Canvas` object to draw the building on the screen.

## Drawing the Streets

Next, we will add the ability to draw simple streets in our city. We'll create a `drawStreet` method that takes in the `Canvas` object, the `x` and `y` coordinates of the starting point of the street, and the street's length.

```dart
void drawStreet(Canvas canvas, double x, double y, double length) {
  final paint = Paint()..color = Colors.grey;

  final path = Path()
    ..moveTo(x, y)
    ..lineTo(x + length, y);

  canvas.drawPath(path, paint);
}
```

The `drawStreet` method creates a `Paint` object with the desired color and a `Path` object that represents a straight line. We then use the `drawPath` method on the `Canvas` object to draw the street.

## Implementing the Drawing Logic

Now that we have the methods to draw buildings and streets, we can implement the drawing logic in the `CityPainter` class.

```dart
void paint(Canvas canvas, Size size) {
  final streetLength = size.width / 2;
  final buildingWidth = size.width / 4;
  final buildingHeight = size.height / 4;

  for (double y = size.height; y > 0; y -= buildingHeight + streetLength) {
    for (double x = 0; x < size.width; x += buildingWidth + streetLength) {
      drawBuilding(canvas, x, y - buildingHeight, buildingWidth, buildingHeight);
    }
  }

  for (double y = size.height - buildingHeight; y > 0; y -= buildingHeight + streetLength) {
    for (double x = 0; x < size.width; x += buildingWidth + streetLength) {
      drawStreet(canvas, x, y, streetLength);
    }
  }
}
```

In the `paint` method, we calculate the length and dimensions of the buildings and streets based on the size of the canvas. We then use nested loops to iterate over the canvas and draw the buildings and streets.

## Running the Application

To see the final result, run the application on a device or emulator using the `flutter run` command. You should see an isometric city with buildings and streets drawn on the screen.

## Conclusion

In this tutorial, we learned how to use the Flutter Canvas to draw an isometric city. We used the CustomPainter class to create a custom painting widget and implemented the drawing logic for buildings and streets. With this knowledge, you can further enhance the city by adding more elements like trees, vehicles, and other structures. Have fun experimenting and creating your own isometric city in Flutter!

**#Flutter #Canvas**