---
layout: post
title: "Using SkiaShadersMask for creating photo filters in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

In this tutorial, we will explore how to use the `SkiaShadersMask` class in Flutter to create custom photo filters. `SkiaShadersMask` is a powerful tool that allows us to apply complex image effects and transformations to our Flutter applications.

## Table of Contents

- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Setting Up the Project](#setting-up-the-project)
- [Applying Photo Filters](#applying-photo-filters)
- [Conclusion](#conclusion)

## Introduction

Photo filters enhance the visual appeal of images by applying various effects such as blurs, gradients, and color adjustments. Flutter provides various options for applying photo filters, including the `SkiaShadersMask` class.

## Prerequisites

To follow along with this tutorial, you will need:

- Flutter SDK installed on your machine
- A code editor of your choice (such as Visual Studio Code)
- Basic knowledge of Flutter and Dart programming

## Setting Up the Project

Let's start by creating a new Flutter project. Open your terminal or command prompt and run the following command:

```bash
flutter create photo_filters_app
cd photo_filters_app
```

Open the project in your preferred code editor and navigate to the `lib/main.dart` file. Replace the existing code with the following:

```dart
import 'dart:ui' as ui;
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';
import 'package:flutter/painting.dart';

void main() {
  runApp(PhotoFiltersApp());
}

class PhotoFiltersApp extends StatefulWidget {
  @override
  _PhotoFiltersAppState createState() => _PhotoFiltersAppState();
}

class _PhotoFiltersAppState extends State<PhotoFiltersApp> {
  ui.Image _image;

  Future<void> loadAssets() async {
    final data = await rootBundle.load('assets/images/sample_photo.jpg');
    final codec = await ui.instantiateImageCodec(data.buffer.asUint8List());
    final frame = await codec.getNextFrame();
    setState(() {
      _image = frame.image;
    });
  }

  @override
  void initState() {
    super.initState();
    loadAssets();
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Photo Filters App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Photo Filters'),
        ),
        body: Center(
          child: _image != null
              ? ShaderMask(
                  shaderCallback: (bounds) {
                    return PictureShader(
                      _image,
                      TileMode.clamp,
                      TileMode.clamp,
                      Matrix4.identity().storage,
                    );
                  },
                  blendMode: BlendMode.softLight,
                  child: Image(
                    image: AssetImage('assets/images/sample_photo.jpg'),
                    fit: BoxFit.cover,
                  ),
                )
              : CircularProgressIndicator(),
        ),
      ),
    );
  }
}
```

In this code, we have defined a `PhotoFiltersApp` widget, which is our main application widget. Inside this widget, we load an image using the `ui.Image` class and display it on the screen. We apply the `ShaderMask` widget to create a photo filter effect using the `PictureShader`.

## Applying Photo Filters

To apply a photo filter using `SkiaShadersMask`, we need to follow these steps:

1. Import the Skia package by adding `import 'dart:ui' as ui;` to the code.
2. Load the image using `rootBundle.load('assets/images/sample_photo.jpg')` and instantiate the image codec using `ui.instantiateImageCodec()`.
3. Retrieve the image frame using `codec.getNextFrame()`.
4. Wrap the `Image` widget with the `ShaderMask` widget.
5. Inside the `shaderCallback` property of `ShaderMask`, create a `PictureShader` using the `_image` and desired `TileMode` and `Matrix4` configuration.
6. Set the `blendMode` property of `ShaderMask` to the desired blend mode.
7. Replace the `AssetImage` object with `AssetImage('assets/images/sample_photo.jpg')`.

## Conclusion

In this tutorial, we explored how to use the `SkiaShadersMask` class in Flutter to create custom photo filters. By applying the `ShaderMask` widget, we were able to transform and enhance the appearance of images in our Flutter applications. Experiment with different `TileMode` and `Matrix4` configurations to achieve the desired effects.

I hope you found this tutorial helpful. Happy Fluttering!

#flutter #photofilters