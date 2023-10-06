---
layout: post
title: "Using SkiaShadersMask for creating image stitching in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

Image stitching is a technique used to combine multiple images into a single panoramic image. In Flutter, we can leverage the Skia library and the `SkiaShadersMask` class to implement image stitching. Skia is a powerful 2D graphics library that provides various shaders and filters to manipulate and compose images.

In this tutorial, we will demonstrate how to use the `SkiaShadersMask` class to stitch two images together in Flutter.

## Prerequisites

To follow along with this tutorial, make sure you have the following:

- Flutter SDK installed on your machine
- A basic understanding of Flutter development

## Steps to Create Image Stitching with SkiaShadersMask

### Step 1: Set Up the Project

Create a new Flutter project using the following command:

```bash
flutter create image_stitching
```

Change the directory to the project folder:

```bash
cd image_stitching
```

### Step 2: Add the Skia Flutter Plugin

To use the `SkiaShadersMask` class, we need to add the `flutter_skia` plugin to the `pubspec.yaml` file in your project. Open the `pubspec.yaml` file and add the following lines:

```yaml
dependencies:
  flutter_skia: ^0.1.0
```

Save the file and run the following command to download the plugin:

```bash
flutter pub get
```

### Step 3: Create the Stitched Image Widget

Create a new Dart file called `stitched_image.dart` and add the following code:

```dart
import 'dart:ui';

import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';
import 'package:flutter_skia/flutter_skia.dart';

class StitchedImage extends StatelessWidget {
  final ImageProvider image1;
  final ImageProvider image2;

  const StitchedImage({required this.image1, required this.image2});

  @override
  Widget build(BuildContext context) {
    return FutureBuilder(
      future: _loadImages(),
      builder: (BuildContext context, AsyncSnapshot<List<SKImage>> snapshot) {
        if (snapshot.connectionState == ConnectionState.done) {
          if (snapshot.hasError) {
            return const Text('Failed to load images');
          }

          final images = snapshot.data;

          return CustomPaint(
            painter: _StitchedImagePainter(images),
          );
        } else {
          return const CircularProgressIndicator();
        }
      },
    );
  }

  Future<List<SKImage>> _loadImages() async {
    final image1Data = await _loadImage(image1);
    final image2Data = await _loadImage(image2);

    return [image1Data, image2Data];
  }

  Future<SKImage> _loadImage(ImageProvider imageProvider) async {
    final completer = Completer<ui.Image>();
    final stream = imageProvider.resolve(const ImageConfiguration());
    stream.addListener(ImageStreamListener((info, _) {
      completer.complete(info.image);
    }));

    final image = await completer.future;
    final codec = await image.toByteData(format: ui.ImageByteFormat.png);
    final data = codec!.buffer.asUint8List();
    final imageSkia = await SKImage.fromEncodedCodec(codec!);

    return imageSkia;
  }
}

class _StitchedImagePainter extends CustomPainter {
  final List<SKImage>? images;

  _StitchedImagePainter(this.images);

  @override
  void paint(Canvas canvas, Size size) {
    if (images != null && images!.length >= 2) {
      final maxImageWidth = size.width / 2;
      final maxImageHeight = size.height;

      final image1 = images![0];
      final image2 = images![1];

      final imageRect1 = Rect.fromLTRB(0, 0, maxImageWidth, maxImageHeight);
      final imageRect2 = Rect.fromLTRB(
        maxImageWidth,
        0,
        size.width,
        maxImageHeight,
      );

      final paint1 = Paint();
      final paint2 = Paint();

      final shader1 = ImageShader(
        image1,
        TileMode.clamp,
        TileMode.clamp,
        Matrix4.identity().storage,
      );
      final shader2 = ImageShader(
        image2,
        TileMode.clamp,
        TileMode.clamp,
        Matrix4.identity().storage,
      );

      paint1.shader = SkiaShadersMask(
        shader2,
        BlendMode.dstOut,
      );
      paint2.shader = SkiaShadersMask(
        shader1,
        BlendMode.srcOver,
      );

      canvas.drawRect(imageRect1, paint1);
      canvas.drawRect(imageRect2, paint2);
    }
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) {
    return true;
  }
}

```

The `StitchedImage` widget takes two image providers (`image1` and `image2`) as parameters. It loads the images using the `flutter_skia` plugin and then uses a custom painter (`_StitchedImagePainter`) to draw the stitched image on the canvas.

### Step 4: Implement Image Stitching

In your main.dart file, update the existing code with the following:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';
import 'package:flutter/foundation.dart';
import 'package:flutter/rendering.dart';
import 'package:flutter/services.dart';
import 'package:flutter_skia/flutter_skia.dart';
import 'stitched_image.dart';

void main() {
  // Enable Skia software rendering for Flutter
  debugDefaultTargetPlatformOverride = TargetPlatform.fuchsia;
  WidgetsFlutterBinding.ensureInitialized();
  SystemChrome.setPreferredOrientations([DeviceOrientation.landscapeLeft]);

  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final image1 = AssetImage('assets/image1.jpg');
    final image2 = AssetImage('assets/image2.jpg');

    return MaterialApp(
      home: Scaffold(
        body: Center(
          child: StitchedImage(
            image1: image1,
            image2: image2,
          ),
        ),
      ),
    );
  }
}
```
Make sure to have two images named "image1.jpg" and "image2.jpg" under an "assets" folder in the root directory of your Flutter project.

### Step 5: Run the App

Save all the changes and run your Flutter app using the following command:

```bash
flutter run
```

You should now see the two images stitched together in a panorama view.

## Conclusion

Using the `SkiaShadersMask` class from the `flutter_skia` package, we can easily implement image stitching in Flutter. By combining different shaders and blending modes, we can manipulate and compose images to create stunning visual effects.

Feel free to explore more advanced usage of the `SkiaShadersMask` class and other Skia shaders to achieve various image manipulation effects in your Flutter applications. Happy coding!

## Tags
#Flutter #ImageStitching