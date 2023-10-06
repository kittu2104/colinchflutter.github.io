---
layout: post
title: "Using SkiaShadersMask for creating image croppers in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

Creating image croppers is a common requirement in many mobile applications. In Flutter, you can achieve this by using the `SkiaShadersMask` class from the Skia package. `SkiaShadersMask` allows you to apply a mask to an image, effectively cropping it to the desired shape.

## Getting Started

To get started, you'll need to add the Skia package to your project's dependencies in the `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  skia: ^0.4.0
```

After adding the package, run `flutter pub get` to download and update your project's dependencies.

## Applying the Mask

Once you have the Skia package installed, you can use the `SkiaShadersMask` class to create an image cropper. 

First, import the necessary classes:

```dart
import 'package:flutter/material.dart';
import 'package:skia/skia.dart';
```

Next, create a custom widget that extends `CustomPainter`:

```dart
class ImageCropper extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final paint = Paint();

    // Create the rectangular mask
    final rect = Rect.fromLTRB(0, 0, size.width, size.height);
    final maskShader = SkiaShadersMask(
      ShaderColor.fromColor(Colors.transparent),
      ShaderColor.fromColor(Colors.white),
    );
    final maskPaint = paint..shader = maskShader.createShader(rect);

    // Draw the mask
    canvas.drawRect(rect, maskPaint);

    // Draw the image
    final image = Image.asset('assets/image.jpg');
    canvas.drawImageRect(
      image.image,
      Rect.fromLTWH(0, 0, image.width.toDouble(), image.height.toDouble()),
      rect,
      paint,
    );
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) {
    return true;
  }
}
```

In the `paint` method, we create a rectangular mask using the `SkiaShadersMask` class. The mask is created with a transparent color as the base and a white color as the highlight. Various other options are available for defining different shapes and styles for the mask.

Next, we set the mask as the shader for the `maskPaint` object. We then draw the mask using `canvas.drawRect()`.

Finally, we draw the image using `canvas.drawImageRect()` with the original image dimensions and the desired cropping rectangle.

## Using the ImageCropper Widget 

To use the `ImageCropper` widget, you can include it in your application as follows:

```dart
class MyImageCropperApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Image Cropper',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Image Cropper'),
        ),
        body: Center(
          child: CustomPaint(
            painter: ImageCropper(),
          ),
        ),
      ),
    );
  }
}

void main() {
  runApp(MyImageCropperApp());
}
```

In this example, we create a simple Flutter application with a `CustomPaint` widget that uses the `ImageCropper` custom painter.

## Conclusion

Using the `SkiaShadersMask` class from the Skia package, we can easily create image croppers in Flutter. By applying a mask to an image, we can control its shape and achieve the desired cropping effect.

By combining this technique with other Flutter features, such as gestures, you can create powerful and versatile image croppers for your mobile applications.

#flutter #cropping-image