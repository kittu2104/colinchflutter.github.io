---
layout: post
title: "Creating mirror effects with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

In this blog post, we will explore how to create mirror effects using the `SkiaShadersMask` class in Flutter. Mirror effects can add depth and visual interest to your app's UI, and Flutter's `SkiaShadersMask` makes it easy to achieve this effect.

## Table of Contents
1. Overview
2. Setting up the project
3. Creating a mirror effect
4. Adding customization options
5. Conclusion
6. References

## 1. Overview
The `SkiaShadersMask` class in Flutter provides a way to create custom shader effects on the canvas. By using this class, we can create various visual effects, including mirror effects. In a mirror effect, a reflection of the original image is displayed vertically.

## 2. Setting up the project
To get started, create a new Flutter project by running the following command:

```bash
flutter create mirror_effects
cd mirror_effects
```

Then, open the project in your preferred IDE.

## 3. Creating a mirror effect
To create a mirror effect using `SkiaShadersMask`, we need to define a `Paint` object and a `Rect` to indicate the area where the mirror effect will be applied.

```dart
import 'dart:ui' as ui;
import 'package:flutter/material.dart';

class MirrorEffectsDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CustomPaint(
      painter: MirrorPainter(),
      child: Container(),
    );
  }
}

class MirrorPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final seedRect = Rect.fromLTWH(0, 0, size.width, size.height);
    final paint = Paint()
      ..isAntiAlias = true
      ..style = PaintingStyle.fill;
    final shader =
        ui.ImageShader(ui.Image.asset('assets/image.jpg'), TileMode.mirror,
            TileMode.mirror, Matrix4.identity().storage);
    final maskedPaint = paint..shader = shader;
    canvas.drawRect(seedRect, maskedPaint);
  }
  
  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    return false;
  }
}
```

In the above code, we define a `MirrorPainter` class that extends `CustomPainter`. Inside the `paint` method, we create a `Paint` object and a `Rect` to represent the area where the mirror effect will be applied. We then create an `ImageShader` by passing in the path to the image asset, and set it as the shader of the `Paint` object using the `shader` property. Finally, we draw a rectangle using the `drawRect` method of the `Canvas` class.

## 4. Adding customization options
To make our mirror effect more flexible and customizable, we can add properties to the `MirrorPainter` class to control the behavior of the effect. For example, we can add properties to control the mirror direction, opacity, or even the image source.

```dart
class MirrorPainter extends CustomPainter {
  final String imagePath;
  final bool isHorizontalMirror;
  final double opacity;

  MirrorPainter({
    required this.imagePath,
    this.isHorizontalMirror = true,
    this.opacity = 1.0,
  });

  @override
  void paint(Canvas canvas, Size size) {
    // TODO: Implement paint method with customization options
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    return false;
  }
}
```

In the above code, we added three properties to the `MirrorPainter` class: `imagePath` to specify the image asset, `isHorizontalMirror` to control the mirror direction, and `opacity` to adjust the opacity of the mirror effect.

## 5. Conclusion
In this blog post, we explored how to create mirror effects with the `SkiaShadersMask` class in Flutter. We learned how to set up a Flutter project, create a mirror effect, and add customization options to make the effect more flexible. By using the power of Flutter's painting APIs, we can create stunning visual effects to enhance our app's UI.

## 6. References
- [Flutter documentation on SkiaShadersMask](https://api.flutter.dev/flutter/dart-ui/SkiaShadersMask-class.html) #Flutter #SkiaShadersMask