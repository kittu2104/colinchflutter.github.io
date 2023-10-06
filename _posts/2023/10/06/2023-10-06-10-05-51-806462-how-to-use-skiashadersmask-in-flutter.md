---
layout: post
title: "How to use SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

SkiaShadersMask is a powerful utility in Flutter that allows you to apply masks to an image or shape using various shader effects. With SkiaShadersMask, you can create eye-catching visual effects and enhance the user interface of your Flutter app. In this tutorial, we will guide you through the process of using SkiaShadersMask in your Flutter project.

## Prerequisites

Before we dive into the usage of SkiaShadersMask, make sure you have the following prerequisites:

- Flutter SDK installed on your machine
- A basic understanding of Flutter widgets and painting in Flutter

## Step 1: Add dependencies

To use SkiaShadersMask in your Flutter project, you need to add the `flutter_skia` package to your `pubspec.yaml` file. Open the `pubspec.yaml` file and add the following line under the `dependencies` section:

```yaml
dependencies:
  flutter_skia: ^0.1.0
```

Save the file and run `flutter pub get` in your project's directory to fetch the package.

## Step 2: Import the required packages

In your Dart file, import the necessary packages for using SkiaShadersMask:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_skia/flutter_skia.dart';
```

## Step 3: Implementing SkiaShadersMask

Now, you can start using SkiaShadersMask in your Flutter app. Let's assume you want to apply a gradient mask to an image. Here's an example code snippet that demonstrates this:

```dart
class MaskedImage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CustomPaint(
      painter: _MaskPainter(),
      child: Image.asset('assets/image.png'),
    );
  }
}

class _MaskPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final imageRect = Rect.fromLTWH(0, 0, size.width, size.height);
    final shader = SkiaShadersMask.createLinearGradient(
      colors: [Colors.black, Colors.transparent],
      stops: [0.0, 1.0],
      end: Alignment.bottomCenter,
    );
    final maskRect = imageRect.inflate(15);

    canvas.saveLayer(imageRect, Paint());
    canvas.drawImageRect(
      img,
      Rect.fromLTRB(0, 0, image.size.width, image.size.height),
      imageRect,
      Paint()..shader = shader,
    );
    canvas.restore();
  }

  @override
  bool shouldRepaint(_MaskPainter oldDelegate) => false;
}
```

In this example, we create a `CustomPainter` that paints a gradient mask on top of an image. We use the `SkiaShadersMask.createLinearGradient` method to create a linear gradient shader with black and transparent colors. The `maskRect` is created by inflating the image's boundaries by 15 pixels. Finally, we save the current canvas state, draw the image with the shader applied, and restore the canvas.

## Conclusion

In this tutorial, you learned how to use SkiaShadersMask in Flutter to apply masks to images and shapes. SkiaShadersMask opens up a world of possibilities for creating visually appealing user interfaces in your Flutter app. Experiment with different shaders and effects to make your app stand out.

For more advanced usage and customization options, refer to the SkiaShadersMask and flutter_skia documentation.

#flutter #flutterdev