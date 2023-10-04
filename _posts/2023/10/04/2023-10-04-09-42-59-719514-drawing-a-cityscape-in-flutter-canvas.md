---
layout: post
title: "Drawing a cityscape in Flutter Canvas"
description: " "
date: 2023-10-04
tags: [setting, creating]
comments: true
share: true
---

In this tutorial, we will explore how to use the Flutter Canvas API to draw a cityscape. We will create a visually pleasing scene with buildings, trees, and a sun. So let's get started!

## Table of Contents
1. [Setting Up the Project](#setting-up-the-project)
2. [Creating the Cityscape](#creating-the-cityscape)
3. [Drawing the Buildings](#drawing-the-buildings)
4. [Adding Trees](#adding-trees)
5. [The Sun](#the-sun)
6. [Conclusion](#conclusion)

## Setting Up the Project <a name="setting-up-the-project"></a>
Before diving into the code, make sure you have Flutter installed and set up on your machine. Create a new Flutter project using the command `flutter create cityscape_project`. Once the project is created, navigate to the `lib` directory and open the `main.dart` file.

## Creating the Cityscape <a name="creating-the-cityscape"></a>
Start by creating a new `CustomPaint` widget inside the `build` method of the `MyApp` class. The `CustomPaint` widget allows us to create a canvas where we can draw our cityscape.

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Cityscape'),
        ),
        body: CustomPaint(
          painter: CityscapePainter(),
        ),
      ),
    );
  }
}
```

## Drawing the Buildings <a name="drawing-the-buildings"></a>
Next, let's create a new class called `CityscapePainter` which will be responsible for painting the cityscape on the canvas. In the `CityscapePainter` class, override the `paint` method and use the `canvas` parameter to draw the buildings.

```dart
class CityscapePainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // Drawing code goes here
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    return true;
  }
}
```

Inside the `paint` method, we can use the `drawRect` method to draw the buildings. Define the coordinates and size of each building, and then use the `canvas.drawRect` method to draw them.

```dart
class CityscapePainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final buildingPaint = Paint()
      ..style = PaintingStyle.fill
      ..color = Colors.grey;

    final building1 = Rect.fromLTWH(50, 200, 100, size.height - 200);
    canvas.drawRect(building1, buildingPaint);

    // Add more buildings here
  }
  
  // ...
}
```

## Adding Trees <a name="adding-trees"></a>
To add trees to our cityscape, we can use the `drawPath` method to draw triangular shapes representing trees. Define the coordinates of each tree and draw them using the `canvas.drawPath` method.

```dart
class CityscapePainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // Building drawing code

    final treePaint = Paint()
      ..style = PaintingStyle.fill
      ..color = Colors.green;

    final treePath = Path();
    treePath.moveTo(300, size.height - 50);
    treePath.lineTo(270, size.height - 150);
    treePath.lineTo(330, size.height - 150);
    treePath.close();
    canvas.drawPath(treePath, treePaint);

    // Add more trees here
  }

  // ...
}
```

## The Sun <a name="the-sun"></a>
To draw the sun, use the `drawCircle` method and set the `color` property of the `Paint` object to a yellow color.

```dart
class CityscapePainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // Building and tree drawing code

    final sunPaint = Paint()
      ..style = PaintingStyle.fill
      ..color = Colors.yellow;

    canvas.drawCircle(Colors.yellow, Offset(size.width - 50, 50), 30, sunPaint);
  }

  // ...
}
```

## Conclusion <a name="conclusion"></a>
You have successfully created a cityscape using the Flutter Canvas API. You learned how to draw buildings, trees, and a sun to create a visually pleasing scene. Experiment with different shapes, colors, and sizes to create your own unique cityscape. Have fun exploring the capabilities of the Flutter Canvas API! #flutter #cityscape