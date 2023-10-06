---
layout: post
title: "Using SkiaShadersMask for creating shadow effects in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

Shadows can add depth and visual appeal to a user interface, making it more engaging and realistic. In Flutter, you can create shadow effects using the `SkiaShadersMask` class from the Flutter `skia` package.

To get started, make sure you have added the `skia` package as a dependency in your Flutter project's `pubspec.yaml` file:

```dart
dependencies:
  skia: ^0.4.1
```

Next, let's see an example of how to use `SkiaShadersMask` to create a shadow effect for a widget in Flutter:

1. Import the necessary packages:

```dart
import 'dart:ui' as ui;
import 'package:flutter/material.dart';
import 'package:flutter/scheduler.dart';
import 'package:skia/shader.dart' as skia;
```

2. Create a custom widget that applies the shadow effect:

```dart
class ShadowWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CustomPaint(
      painter: ShadowPainter(),
      child: Container(
        width: 200,
        height: 200,
        color: Colors.white,
      ),
    );
  }
}
```

3. Implement the `CustomPainter` class to define the shadow effect:

```dart
class ShadowPainter extends CustomPainter {
  @override
  void paint(ui.Canvas canvas, ui.Size size) {
    final paint = ui.Paint()
      ..style = ui.PaintingStyle.fill
      ..shader = skia.SkiaShadersMask(
        MaskFilter.blur(BlurStyle.normal, 10),
        skia.Color.fromARGB(100, 0, 0, 0),
      )
      ..maskFilter = MaskFilter.blur(BlurStyle.normal, 10);

    final rect = ui.Rect.fromLTWH(0, 0, size.width, size.height);
    canvas.drawRect(rect, paint);
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) => false;
}
```

In the code above, we define a custom painter (`ShadowPainter`) that applies the shadow effect. We set up a paint object with the desired `shader` and `maskFilter` properties. The `SkiaShadersMask` shader creates a shadow effect with blur using the `MaskFilter.blur` method with a specified radius. We use `Color.fromARGB` to set the shadow color and transparency level.

4. Finally, use the `ShadowWidget` in your Flutter application:

```dart
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: Center(
          child: ShadowWidget(),
        ),
      ),
    );
  }
}
```

Now, when you run your Flutter application, you should see a square widget with a shadow effect applied to it.

Remember to customize the shadow effect properties such as the blur radius, color, and transparency to achieve your desired design.

That's it! You have successfully used `SkiaShadersMask` to create a shadow effect in Flutter. Experiment with different parameters to create various shadow styles and effects for your UI elements.

#flutter #shadoweffects