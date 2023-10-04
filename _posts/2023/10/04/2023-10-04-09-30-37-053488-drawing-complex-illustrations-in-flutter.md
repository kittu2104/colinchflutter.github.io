---
layout: post
title: "Drawing complex illustrations in Flutter"
description: " "
date: 2023-10-04
tags: [introduction), setting]
comments: true
share: true
---

In this blog post, we will explore how to create complex illustrations in Flutter, a popular cross-platform UI toolkit. Flutter provides a powerful canvas widget called `CustomPaint` that allows us to draw custom shapes, paths, and images. With the help of this widget and Flutter's rich set of painting APIs, we can create intricate and visually appealing illustrations.

## Table of Contents
- [Introduction](#introduction)
- [Setting up the Project](#setting-up-the-project)
- [Drawing Basic Shapes](#drawing-basic-shapes)
- [Creating Paths and Curves](#creating-paths-and-curves)
- [Drawing Images](#drawing-images)
- [Applying Animations](#applying-animations)
- [Conclusion](#conclusion)

## Introduction
Creating complex illustrations often requires a lot of control over the drawing procedures. Flutter's `CustomPaint` widget provides a canvas on which we can paint our custom visuals. Flutter's painting APIs offer various tools to create shapes, paths, curves, and handle images, enabling us to design intricate and detailed illustrations.

## Setting up the Project
To get started, we need to set up a Flutter project. Open your favorite code editor and create a new Flutter project. Make sure you have Flutter and Dart installed on your development environment.

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Complex Illustrations',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Drawing Complex Illustrations'),
      ),
      body: Center(
        child: CustomPaint(
          painter: MyPainter(),
        ),
      ),
    );
  }
}

class MyPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size){
    // Implement custom drawing logic here
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    return true;
  }
}
```

This is a basic setup for our Flutter project. We define a `CustomPainter` class that extends the `CustomPainter` base class. We override the `paint` method to perform our custom drawing logic. Now, let's dive into the actual drawing.

## Drawing Basic Shapes

Flutter provides a set of basic shape classes, such as `Rect`, `Circle`, `RoundedRectangle`, and more. We can create instances of these classes and use them to draw shapes on the canvas.

```dart
@override
void paint(Canvas canvas, Size size){
  final rect = Rect.fromLTWH(100, 100, 200, 200);
  final paint = Paint()
    ..color = Colors.blue
    ..style = PaintingStyle.fill;

  canvas.drawRect(rect, paint);
}
```

In the code snippet above, we created a `Rect` object with the position (100, 100) and dimensions 200x200. We also defined a `Paint` object with a blue color and the `fill` style. Finally, we used the `drawRect` method of the canvas to draw the rectangle on the canvas with the given paint object.

You can also draw other shapes like circles, rounded rectangles, and polygons using similar methods like `drawCircle` or `drawRRect`. By combining these basic shapes, you can create more complex illustrations.

## Creating Paths and Curves

Sometimes, basic shapes are not enough to create complex illustrations. Flutter provides a `Path` class that allows us to create custom paths and curves. We can define points on the canvas and connect them using straight lines or curves.

```dart
@override
void paint(Canvas canvas, Size size){
  final path = Path()
    ..moveTo(100, 100)
    ..lineTo(200, 200)
    ..quadraticBezierTo(300, 100, 400, 200)
    ..cubicTo(350, 300, 250, 300, 200, 200);

  final paint = Paint()
    ..color = Colors.red
    ..style = PaintingStyle.stroke
    ..strokeWidth = 2.0;

  canvas.drawPath(path, paint);
}
```

In the example above, we defined a path with multiple points using `moveTo`, `lineTo`, `quadraticBezierTo`, and `cubicTo` methods. We created a Paint object with a red color, set its style to `stroke`, and defined the stroke width. Finally, we used the `drawPath` method to draw the path on the canvas.

By manipulating points and using different curve types like quadratic or cubic Bezier curves, we can create complex and organic-looking shapes.

## Drawing Images

To include images in your complex illustrations, Flutter provides the `drawImage` method. You can load an image using `AssetImage` or network images using `NetworkImage`. Once you have the image loaded, you can draw it on the canvas.

```dart
@override
void paint(Canvas canvas, Size size){
  final image = AssetImage('assets/my_image.png');
  final imageRect = Rect.fromLTWH(100, 100, 200, 200);

  final paint = Paint();
  canvas.drawImageRect(image, imageRect, paint);
}
```

In the example above, we loaded an image using `AssetImage` and defined a rectangle to specify the position and dimensions of the image on the canvas. Finally, we used the `drawImageRect` method to draw the image on the canvas.

You can resize the image, rotate it, or apply various image effects using the `Rect`, `paint`, and `drawImageRect` methods to achieve more creative illustrations.

## Applying Animations

Flutter also allows us to animate our illustrations using the animation framework. By creating animations and updating the state of our custom painter, we can achieve dynamic and interactive illustrations.

```dart
class MyPainter extends CustomPainter with SingleTickerProviderStateMixin {
  AnimationController animationController;

  @override
  void initState() {
    super.initState();
    animationController = AnimationController(
      vsync: this,
      duration: Duration(seconds: 2),
    )..repeat();
  }

  @override
  void dispose() {
    animationController?.dispose();
    super.dispose();
  }

  @override
  void paint(Canvas canvas, Size size){
    final animationValue = animationController.value;
    // Use the animation value to animate the illustration

    // Update the canvas every frame as the animation progresses
    animationController.addListener(() {
      canvas.clear();
      paint(canvas, size);
    });
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    return false;
  }
}
```

In the code snippet above, we added animation functionality to our custom painter using `SingleTickerProviderStateMixin`. We created an `AnimationController` with a duration and repeat. Inside the `paint` method, we use the animation value to animate our illustration. We also added a listener to the animationController to repaint the canvas every frame.

By utilizing Flutter's powerful animation framework, we can bring our illustrations to life and create captivating user experiences.

## Conclusion

In this blog post, we explored how to create complex illustrations in Flutter using the `CustomPaint` widget and Flutter's rich set of painting APIs. We learned how to draw basic shapes, create custom paths and curves, incorporate images, and apply animations. With these techniques, you can create visually stunning and interactive illustrations in your Flutter apps.

#flutter #illustrations