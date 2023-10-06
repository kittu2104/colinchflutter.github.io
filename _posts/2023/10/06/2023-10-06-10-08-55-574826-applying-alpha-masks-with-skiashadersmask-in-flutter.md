---
layout: post
title: "Applying alpha masks with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

In Flutter, you can apply alpha masks to your images or widgets to create interesting effects and blend them with the underlying background. SkiaShadersMask is a powerful class in Skia library that allows you to achieve this. In this tutorial, we will explore how to use SkiaShadersMask to apply alpha masks in Flutter.

## Prerequisites
To follow this tutorial, make sure you have Flutter installed on your machine. You can install Flutter by following the instructions on the official Flutter website.

## Adding Skia library to your Flutter project
Flutter uses the Skia library to provide low-level rendering capabilities. To use SkiaShadersMask, you need to add the Flutter Skia package to your project. Open your project's `pubspec.yaml` file and add the following dependency:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_skia: ^0.4.0
```

Save the file and run `flutter pub get` to fetch the dependency.

## Using SkiaShadersMask

1. Import the necessary libraries in your Dart file:

```dart
import 'dart:ui' as ui;
import 'package:flutter/material.dart';
import 'package:flutter/rendering.dart';
import 'package:flutter_skia/flutter_skia.dart';
```

2. Create a custom widget to apply the alpha mask:

```dart
class AlphaMaskWidget extends StatefulWidget {
  final Widget child;
  final ImageProvider maskImageProvider;

  AlphaMaskWidget({required this.child, required this.maskImageProvider});

  @override
  _AlphaMaskWidgetState createState() => _AlphaMaskWidgetState();
}

class _AlphaMaskWidgetState extends State<AlphaMaskWidget> {
  late ui.Image? _maskImage;

  @override
  void initState() {
    super.initState();
    widget.maskImageProvider.resolve(ImageConfiguration()).addListener(
      ImageStreamListener((info, syncCall) async {
        final image = await info.image.toByteData(format: ui.ImageByteFormat.png);
        final decodedImage = await decodeImageFromList(image!.buffer.asUint8List());
        setState(() {
          _maskImage = decodedImage;
        });
      }),
    );
  }

  @override
  Widget build(BuildContext context) {
    if (_maskImage == null) {
      return widget.child;
    }
    
    return CustomPaint(
      foregroundPainter: _AlphaMaskPainter(_maskImage!),
      child: widget.child,
    );
  }
}

class _AlphaMaskPainter extends CustomPainter {
  final ui.Image maskImage;

  _AlphaMaskPainter(this.maskImage);

  @override
  void paint(Canvas canvas, Size size) {
    final imageSize = Size(maskImage.width.toDouble(), maskImage.height.toDouble());
    final rect = Offset.zero & size;
    final maskFit = MaskFit.cover;

    final shader = ui.ImageShader(
      maskImage,
      maskFit == MaskFit.cover ? TileMode.clamp : TileMode.repeated,
      TileMode.clamp,
      Matrix4().storage,
    );

    final paint = Paint()
      ..shader = ui.MojoShader(shader)
      ..style = PaintingStyle.fill;

    canvas.drawRect(rect, paint);
  }

  @override
  bool shouldRepaint(_AlphaMaskPainter oldDelegate) {
    return maskImage != oldDelegate.maskImage;
  }
}
```

3. Use the AlphaMaskWidget in your app:

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Alpha Mask Demo',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Alpha Mask Demo'),
        ),
        body: SafeArea(
          child: AlphaMaskWidget(
            maskImageProvider: AssetImage('assets/mask.png'),
            child: Container(
              width: double.infinity,
              height: double.infinity,
              color: Colors.blue,
              child: Center(
                child: Text(
                  'Hello, Flutter!',
                  style: TextStyle(
                    fontSize: 24,
                    color: Colors.white,
                  ),
                ),
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```

Replace `'assets/mask.png'` with the path to your own alpha mask image.

4. Run your app:

```bash
flutter run
```

## Conclusion
By using SkiaShadersMask, you can easily apply alpha masks to your images or widgets in Flutter. This allows you to create visually stunning effects and enhance the user experience of your app. Experiment with different alpha mask images and blend them with various backgrounds to achieve the desired effect.