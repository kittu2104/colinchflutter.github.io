---
layout: post
title: "Drawing optical illusions in Flutter"
description: " "
date: 2023-10-04
tags: [creating, drawing]
comments: true
share: true
---

Optical illusions are fascinating visual phenomena that trick our brain and perception. They can be created using various techniques and patterns. In this article, we will explore how to draw optical illusions using the Flutter framework, which allows us to create beautiful and interactive user interfaces.

## Table of Contents
- [Creating a Custom Painter](#creating-a-custom-painter)
- [Drawing Lines and Shapes](#drawing-lines-and-shapes)
- [Implementing Optical Illusions](#implementing-optical-illusions)
- [Conclusion](#conclusion)

## Creating a Custom Painter

In Flutter, we can create custom drawings using the `CustomPainter` class. This class provides a `paint` method that allows us to specify how to draw our custom shapes and patterns. To get started, we need to create a new class that extends `CustomPainter`:

```dart
class OpticalIllusionPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    
  }

  @override
  bool shouldRepaint(OpticalIllusionPainter oldDelegate) {
    return false;
  }
}
```

## Drawing Lines and Shapes

To draw lines and shapes in Flutter, we can use the `canvas.drawLine` and `canvas.drawPath` methods provided by the `Canvas` class. These methods allow us to specify the starting and ending points of the line or the path to be drawn. For example, we can draw a line from `(x1, y1)` to `(x2, y2)` as follows:

```dart
canvas.drawLine(Offset(x1, y1), Offset(x2, y2), paint);
```

We can also draw different shapes by defining a `Path` object and adding lines or curves to it. Once the path is defined, we can use `canvas.drawPath` to draw the shape on the canvas. For example, to draw a triangle, we can do the following:

```dart
Path triangle = Path()
  ..moveTo(x1, y1)
  ..lineTo(x2, y2)
  ..lineTo(x3, y3)
  ..close();

canvas.drawPath(triangle, paint);
```

## Implementing Optical Illusions

Once we have a basic understanding of drawing lines and shapes in Flutter, we can start implementing different optical illusions. There are numerous optical illusions, such as the famous "checker shadow illusion" or the "Müller-Lyer illusion".

For example, to create the checker shadow illusion, we can draw a grid of squares and vary the color intensity of some squares to give the illusion of shadows casted on them. We can use a combination of `canvas.drawRect` and `canvas.drawRectRRect` methods to draw the squares and apply shadows.

```dart
void paint(Canvas canvas, Size size) {
  // Draw the grid of squares
  for (int i = 0; i < numRows; i++) {
    for (int j = 0; j < numColumns; j++) {
      final rect = Rect.fromLTWH(
        j * squareSize,
        i * squareSize,
        squareSize,
        squareSize,
      );
      
      // Vary the color intensity of the squares
      if ((i + j) % 2 == 0) {
        canvas.drawRect(rect, darkPaint);
      } else {
        canvas.drawRect(rect, lightPaint);
      }
    }
  }
  
  // Draw the shadows
  // ...
}
```

We can experiment with different illusions by combining various shapes and patterns. Flutter's powerful drawing capabilities make it easy to create mesmerizing optical illusions.

## Conclusion

Drawing optical illusions in Flutter allows us to explore the fascinating nature of visual perception and create visually engaging experiences for our users. By using the `CustomPainter` class and the drawing methods provided by the `Canvas` class, we can implement various illusions and experiment with different patterns and shapes. The only limit is our creativity!

Remember to share your creative optical illusions with the Flutter community and use `#Flutter` and `#OpticalIllusions` when posting your creations on social media to reach a wider audience. Happy drawing!