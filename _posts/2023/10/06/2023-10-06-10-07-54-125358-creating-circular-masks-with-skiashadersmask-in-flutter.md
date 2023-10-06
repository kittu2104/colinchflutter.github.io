---
layout: post
title: "Creating circular masks with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

In Flutter, you can create circular masks using the `SkiaShadersMask` class from the `flutter_skia` package. This allows you to apply circular masks to images, widgets, or any other UI element in your Flutter application.

## Prerequisites

Before using `SkiaShadersMask`, make sure you have the `flutter_skia` package added as a dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_skia: ^x.x.x
```

Replace `x.x.x` with the latest version of the `flutter_skia` package.

## Usage

To create a circular mask using `SkiaShadersMask`, follow these steps:

**Step 1:** Import the necessary packages:

```dart
import 'dart:ui' as ui;
import 'package:flutter/material.dart';
import 'package:flutter_skia/flutter_skia.dart';
```

**Step 2:** Create a custom widget that extends `CustomPainter`. This widget will be used to draw the circular mask:

```dart
class CircularMaskPainter extends CustomPainter {
  @override
  void paint(ui.Canvas canvas, ui.Size size) {
    final paint = ui.Paint()..color = const ui.Color(0xFF000000);
    canvas.drawCircle(
      Offset(size.width / 2, size.height / 2),
      size.width / 2,
      paint,
    );
  }

  @override
  bool shouldRepaint(CircularMaskPainter oldDelegate) => false;
}
```

**Step 3:** Use the `SkiaShadersMask` widget to apply the circular mask to your desired UI element. Wrap the target widget with the `SkiaShadersMask` widget and provide an instance of your custom painter as the `maskPainter` property:

```dart
SkiaShadersMask(
  maskPainter: CircularMaskPainter(),
  child: // your UI element here,
)
```

For example, to apply the circular mask to an image widget, you can do the following:

```dart
SkiaShadersMask(
  maskPainter: CircularMaskPainter(),
  child: Image.asset('assets/image.png'),
)
```

That's it! Now your UI element will be displayed with a circular mask applied to it.

## Conclusion

In this blog post, you learned how to create circular masks with `SkiaShadersMask` in Flutter. This technique can be useful for adding a stylish touch to your UI elements. Experiment with different sizes and colors to customize the circular masks according to your application's design.

Remember to import the necessary packages, create a custom painter, and wrap your desired UI element with the `SkiaShadersMask` widget. Enjoy creating beautiful circular masks in your Flutter applications!

#flutter #UI #FlutterDevelopment