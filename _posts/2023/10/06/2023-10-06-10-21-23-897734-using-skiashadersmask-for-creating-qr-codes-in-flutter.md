---
layout: post
title: "Using SkiaShadersMask for creating QR codes in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

In this tutorial, we will explore how to create QR codes in Flutter using the SkiaShadersMask library. SkiaShadersMask is a powerful library that allows us to apply custom shaders to create complex visual effects in Flutter.

## Table of Contents
- [What is SkiaShadersMask?](#what-is-skiashadersmask)
- [Installing SkiaShadersMask](#installing-skiashadersmask)
- [Creating a QR Code](#creating-a-qr-code)
- [Applying the Skia Shader](#applying-the-skia-shader)
- [Conclusion](#conclusion)

## What is SkiaShadersMask?

SkiaShadersMask is a Flutter package that provides a set of shaders that can be applied to various graphic components. It is built on top of `skia` library, which is a 2D graphics library used in Google Chrome, Android, and Flutter.

## Installing SkiaShadersMask

To install SkiaShadersMask, add the following line to your `pubspec.yaml` file:

```yaml
dependencies:
  skia_shaders_mask: ^1.0.0
```

Then, run `flutter pub get` to fetch the package.

## Creating a QR Code

To create a QR code in Flutter, we can use the `qr_flutter` package. Add the following line to your `pubspec.yaml` file to install the package:

```yaml
dependencies:
  qr_flutter: ^4.0.0
```

Import the `qr_flutter` package in your Dart file:

```dart
import 'package:qr_flutter/qr_flutter.dart';
```

Now, we can create a QR code widget using the `QrImage` class:

```dart
QrImage(
  data: 'https://www.example.com',
  version: QrVersions.auto,
  size: 200.0,
),
```

Replace the `https://www.example.com` URL with your desired QR code content.

## Applying the Skia Shader

To apply the Skia shader to the created QR code, we need to wrap it with the `ShaderMask` widget from the `flutter` package. First, import the package:

```dart
import 'package:flutter/material.dart';
```

Then, wrap the QR code widget with `ShaderMask`:

```dart
ShaderMask(
  shaderCallback: (Rect bounds) {
    return RadialGradient(
      center: Alignment.center,
      radius: 0.6,
      colors: [
        Colors.red,
        Colors.orange,
      ],
      stops: [0.5, 1.0],
    ).createShader(bounds);
  },
  child: QrImage(
    data: 'https://www.example.com',
    version: QrVersions.auto,
    size: 200.0,
  ),
),
```

In this example, we are applying a radial gradient shader to the QR code, which creates a colorful effect. Feel free to experiment with different shaders and parameters to achieve your desired effect.

## Conclusion

SkiaShadersMask is a powerful library that allows us to create visually appealing QR codes in Flutter. By applying custom Skia shaders to the QR code, we can achieve unique effects and enhance the user experience. Explore the SkiaShadersMask documentation to learn more about the available shaders and their parameters.

#flutter #qrcode