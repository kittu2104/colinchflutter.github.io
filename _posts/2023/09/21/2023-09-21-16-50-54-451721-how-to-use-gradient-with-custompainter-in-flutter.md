---
layout: post
title: "How to use Gradient with CustomPainter in Flutter"
description: " "
date: 2023-09-21
tags: [custompainter, gradient]
comments: true
share: true
---

In Flutter, the **CustomPainter** class allows you to create your own custom shapes and designs by defining the painting behavior. You can use gradients to add beautiful color transitions to your custom shapes. This tutorial will show you how to use gradients with **CustomPainter** in Flutter.

## Step 1: Create a CustomPainter

First, create a new class that extends **CustomPainter**. This class will be responsible for painting the custom shape on the canvas:

```dart
class MyCustomPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // Implement your custom shape painting logic here
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    return true;
  }
}
```

## Step 2: Add Gradient to CustomPainter

To add a gradient to your custom shape, you can use the **LinearGradient** or **RadialGradient** class provided by Flutter. Here is an example of using a linear gradient:

```dart
class MyCustomPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final gradient = LinearGradient(
      colors: [Colors.red, Colors.blue],
      begin: Alignment.topLeft,
      end: Alignment.bottomRight,
    );

    final rect = Rect.fromLTWH(0, 0, size.width, size.height);
    final paint = Paint()..shader = gradient.createShader(rect);

    canvas.drawRect(rect, paint);
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    return true;
  }
}
```

In this example, we create a linear gradient that transitions from red to blue, with the gradient starting from the top-left corner and ending at the bottom-right corner. We then create a **Paint** object and set its shader property to the gradient shader created from the **LinearGradient**. Finally, we use the **drawRect** method of the **Canvas** class to draw a rectangle with the gradient paint.

## Step 3: Use CustomPainter in Flutter Widget

To use the **CustomPainter** with the gradient in a Flutter widget, you can use the **CustomPaint** widget:

```dart
class MyCustomShapeWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CustomPaint(
      painter: MyCustomPainter(),
      child: Container(),
    );
  }
}
```

In the **build** method of your widget, simply wrap the **CustomPaint** widget around any other widget (in this example, **Container** is used as a placeholder). Pass an instance of your **MyCustomPainter** class to the **painter** property of **CustomPaint**.

## Conclusion

Using gradients with **CustomPainter** in Flutter allows you to create beautiful custom shapes with smooth color transitions. By following the steps outlined in this tutorial, you can easily incorporate gradients into your custom painting logic. Experiment with different gradient configurations to achieve the desired visual effects.

#flutter #custompainter #gradient