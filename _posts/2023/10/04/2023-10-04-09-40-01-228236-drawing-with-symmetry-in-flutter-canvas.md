---
layout: post
title: "Drawing with symmetry in Flutter Canvas"
description: " "
date: 2023-10-04
tags: [creating, understanding]
comments: true
share: true
---

When creating a custom drawing in Flutter using the `CustomPaint` widget and `Canvas`, you have the ability to draw symmetrically by leveraging mathematical operations. Symmetry adds an interesting and visually appealing element to your artwork. In this tutorial, we will explore how to achieve symmetry in your Flutter canvas drawings.

## Table of Contents
- [Creating a CustomPaint Widget](#creating-a-custompaint-widget)
- [Understanding Symmetry](#understanding-symmetry)
- [Drawing with Symmetry](#drawing-with-symmetry)
- [Example Code](#example-code)
- [Conclusion](#conclusion)

### Creating a CustomPaint Widget

To get started with drawing on the canvas, you need to use the `CustomPaint` widget. It allows you to define a custom painting behavior by overriding the `paint` method. Inside the `paint` method, you will have access to a `Canvas` object, on which you can draw your artwork.

```dart
CustomPaint(
  painter: MyPainter(),
),
```

### Understanding Symmetry

Symmetry is the concept of mirroring an object or shape across a given axis, resulting in an identical or mirrored image. In drawing, we can achieve symmetry by drawing one half of the object and then mirroring it to create the complete shape.

The axis of symmetry can be vertical, horizontal, or diagonal. The choice of axis depends on the object you are drawing and the desired effect.

### Drawing with Symmetry

To draw symmetrically on the canvas, you can follow these steps:

1. Determine the axis of symmetry for your object.
2. Draw one half of the object on the canvas.
3. Apply a transformation to mirror the first half to the other side of the axis.

For example, if you want to draw a symmetric circle:

```dart
class MyPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final paint = Paint()..color = Colors.blue;
    final radius = size.width / 4;
    final center = Offset(size.width / 2, size.height / 2);
    
    canvas.drawCircle(center, radius, paint);
    
    canvas.save();
    canvas.scale(-1, 1); // Mirroring the canvas horizontally
    canvas.drawCircle(center, radius, paint);
    canvas.restore();
  }
  
  @override
  bool shouldRepaint(CustomPainter oldDelegate) => false;
}
```

In the above example, we draw the first half of the circle using the `drawCircle` method. Then, we mirror the canvas horizontally using the `scale` method and draw the second half. Finally, we restore the canvas to its original transformation using `restore`.

You can apply similar techniques to achieve symmetry with other shapes like squares, triangles, or even complex patterns.

### Example Code

You can try out the following example code to draw a symmetric pattern in Flutter:

```dart
class MyPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final paint = Paint()..color = Colors.red;
    final path = Path()
      ..moveTo(0, size.height / 2)
      ..cubicTo(
        size.width / 4, size.height / 4,
        size.width / 2, size.height / 8,
        size.width, size.height / 2,
      );
    
    canvas.drawPath(path, paint);
    
    canvas.save();
    canvas.scale(-1, 1); // Mirroring the canvas horizontally
    canvas.drawPath(path, paint);
    canvas.restore();
  }
  
  @override
  bool shouldRepaint(CustomPainter oldDelegate) => false;
}

CustomPaint(
  painter: MyPainter(),
),
```

### Conclusion

By understanding the concept of symmetry and utilizing transformation operations, you can create visually stunning and balanced designs in your Flutter canvas drawings. Experiment with different shapes and axes of symmetry to unleash your creativity.

Remember, symmetry is just one technique you can use to enhance your canvas drawings. Feel free to explore other possibilities and combine different techniques to achieve unique and beautiful artwork.