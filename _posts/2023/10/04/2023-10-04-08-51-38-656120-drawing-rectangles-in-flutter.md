---
layout: post
title: "Drawing rectangles in Flutter"
description: " "
date: 2023-10-04
tags: [drawing]
comments: true
share: true
---

Flutter is a powerful framework for building cross-platform mobile applications. One common task in mobile app development is drawing rectangles on the screen. In this post, we will explore different methods to draw rectangles in Flutter.

## 1. Using the Container Widget

The easiest way to draw rectangles in Flutter is by using the `Container` widget. The `Container` widget provides a simple way to create rectangular shapes with customizable properties such as color, border, and padding.

```dart
Container(
  width: 200,
  height: 100,
  color: Colors.blue,
  // Optional border properties
  // border: Border.all(color: Colors.red, width: 2),
  // borderRadius: BorderRadius.circular(10),
)
```

By specifying the `width` and `height` properties of the `Container` widget, you can control the size of the rectangle. The `color` property allows you to set the background color of the rectangle. Optionally, you can add a border to the rectangle by uncommenting the `border` and `borderRadius` properties.

## 2. Custom Painting

If you need more control over the appearance of the rectangle, you can use the `CustomPaint` widget in Flutter. With `CustomPaint`, you can define your own custom painting logic to draw rectangles.

```dart
class RectanglePainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final paint = Paint()
      ..color = Colors.green
      ..style = PaintingStyle.fill;

    final Rect rect = Rect.fromLTRB(50, 50, 250, 150);
    canvas.drawRect(rect, paint);
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    return false;
  }
}
```

In the example above, we define a custom painter class called `RectanglePainter`. In the `paint` method, we use the `Canvas` and `Paint` objects to draw a rectangle with a specific color and style. 

To use the `RectanglePainter` in your Flutter app, you can provide it as the `painter` argument to the `CustomPaint` widget:

```dart
CustomPaint(
  painter: RectanglePainter(),
  child: Container(),
)
```

## Conclusion

Drawing rectangles in Flutter is a straightforward task. The `Container` widget provides a simple way to create rectangular shapes with customizable properties. For more advanced customization, you can use the `CustomPaint` widget and define your own custom painting logic. By leveraging these techniques, you can create beautiful and visually appealing rectangles in your Flutter apps.

Keep in mind that the examples provided in this post are just starting points. Feel free to experiment and explore more advanced features of Flutter to create unique and impressive rectangle designs for your mobile applications.

\#flutter #drawing-rectangles