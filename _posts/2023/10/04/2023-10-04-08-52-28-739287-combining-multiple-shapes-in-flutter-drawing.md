---
layout: post
title: "Combining multiple shapes in Flutter drawing"
description: " "
date: 2023-10-04
tags: [using, using]
comments: true
share: true
---

When working with Flutter, you may often come across situations where you need to combine multiple shapes to create complex drawings or designs. Flutter provides a powerful and flexible framework for graphics rendering, which makes it relatively easy to achieve this.

In this blog post, we will explore different approaches to combine multiple shapes in Flutter and create visually appealing drawings. Let's dive in!

## Table of Contents
- [Using CustomPainter](#using-custompainter)
- [Using Stack Widget](#using-stack-widget)
- [Conclusion](#conclusion)

## Using CustomPainter {#using-custompainter}

Flutter provides a built-in class called `CustomPainter` that allows you to define custom drawing operations. You can subclass `CustomPainter` and override its `paint()` method to perform your drawing logic.

To combine multiple shapes, you can create a `CustomPainter` that draws each shape individually and then use the `paint()` method to call the drawing logic for each shape. Here's an example:

```dart
import 'package:flutter/material.dart';

class CombinedShapesPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // Paint the first shape
    Paint shape1Paint = Paint()..color = Colors.red;
    canvas.drawRect(Rect.fromLTWH(0, 0, size.width, size.height), shape1Paint);

    // Paint the second shape
    Paint shape2Paint = Paint()..color = Colors.blue;
    Offset center = Offset(size.width / 2, size.height / 2);
    canvas.drawCircle(center, size.width / 4, shape2Paint);
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) {
    return false;
  }
}

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      body: Center(
        child: CustomPaint(
          painter: CombinedShapesPainter(),
          child: Container(
            width: 200,
            height: 200,
          ),
        ),
      ),
    ),
  ));
}
```

In the above code, we have created a `CustomPainter` subclass called `CombinedShapesPainter`. In the `paint()` method, we have used `Canvas` to draw a rectangle and a circle with different colors.

To use the `CombinedShapesPainter`, we have wrapped it inside the `CustomPaint` widget and provided it with a `Container` as a child. This allows us to control the size and position of the drawing.

## Using Stack Widget {#using-stack-widget}

Another approach to combining multiple shapes is to use the `Stack` widget. The `Stack` widget allows you to stack multiple widgets on top of each other, making it suitable for situations where you need to overlay shapes.

To use this approach, you can create separate widgets for each shape and stack them using the `Stack` widget. Here's an example:

```dart
import 'package:flutter/material.dart';

class CombinedShapes extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Center(
      child: Stack(
        children: [
          Positioned.fill(
            child: Container(
              color: Colors.red,
            ),
          ),
          Positioned(
            top: 50,
            left: 50,
            child: Container(
              width: 100,
              height: 100,
              decoration: BoxDecoration(
                shape: BoxShape.circle,
                color: Colors.blue,
              ),
            ),
          ),
        ],
      ),
    );
  }
}

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      body: CombinedShapes(),
    ),
  ));
}
```

In the above code, we have created two separate `Container` widgets for each shape. The first `Container` is a full-sized rectangle with a red background, and the second `Container` is a circular shape with a blue background.

We have used the `Stack` widget to stack both containers on top of each other. We have also used the `Positioned` widget to position the circular shape at a specific position within the stack.

## Conclusion {#conclusion}

Combining multiple shapes in Flutter drawing can be achieved through various approaches. The `CustomPainter` class allows you to define custom drawing operations, while the `Stack` widget provides a convenient way to overlay shapes.

Choose the approach that best suits your needs based on the complexity of the shapes and the desired interaction between them. Experiment with different techniques and unleash your creativity when it comes to combining shapes in Flutter!

Happy coding! 🚀

## #Flutter #Drawing