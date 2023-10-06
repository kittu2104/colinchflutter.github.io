---
layout: post
title: "Applying paint splash effects with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

In this tutorial, we will explore how to apply paint splash effects to an image using the `SkiaShadersMask` class in Flutter. The `SkiaShadersMask` class is a part of the Skia graphics engine, which is used by Flutter to provide advanced rendering capabilities.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Setting up the project](#setting-up-the-project)
- [Applying the paint splash effect](#applying-the-paint-splash-effect)
- [Conclusion](#conclusion)
- [Hashtags](#hashtags)

## Prerequisites

Before we begin, make sure you have Flutter and its dependencies installed on your machine. You should also have a basic understanding of Flutter development.

## Setting up the project

To get started, create a new Flutter project using the following command:

`flutter create paint_splash_effects`

Open the project in your preferred code editor.

## Applying the paint splash effect

1. Add an image to the project's `assets/images/` directory that you want to apply the paint splash effect to. For this example, let's use an image named `image.jpg`.

2. Update the `pubspec.yaml` file to include the image asset:

```yaml
flutter:
  assets:
    - assets/images/image.jpg
```

3. Open the `lib/main.dart` file and replace the default code with the following:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';
import 'dart:ui' as ui;

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Paint Splash Effects',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: PaintSplashScreen(),
    );
  }
}

class PaintSplashScreen extends StatefulWidget {
  @override
  _PaintSplashScreenState createState() => _PaintSplashScreenState();
}

class _PaintSplashScreenState extends State<PaintSplashScreen> {
  ImageProvider imageProvider;
  Shader splashShader;

  @override
  void initState() {
    super.initState();
    loadAssets();
  }

  Future<void> loadAssets() async {
    final ByteData byteData = await rootBundle.load('assets/images/image.jpg');
    final Uint8List imageData = byteData.buffer.asUint8List();
    final ui.Codec codec = await ui.instantiateImageCodec(imageData);
    final ui.Image image = await codec.getNextFrame().then((frame) => frame.image);
    imageProvider = MemoryImage(imageData);
    setState(() {
      splashShader = SkiaShadersMask.create(image);
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Paint Splash Effects"),
      ),
      body: Center(
        child: ShaderMask(
          shaderCallback: (Rect bounds) {
            return splashShader;
          },
          child: Image(
            image: imageProvider,
          ),
        ),
      ),
    );
  }
}
```

4. Save the file, and run the project using `flutter run` in the terminal. You should now see the image with the paint splash effect applied.

## Conclusion

In this tutorial, we explored how to apply paint splash effects to an image in Flutter using the `SkiaShadersMask` class. You can modify the code and experiment with different effects and images to create unique visuals in your Flutter applications.

Give it a try and see what creative designs you can come up with!

## Hashtags

#Flutter #PaintSplashEffects