---
layout: post
title: "Applying silhouette effects with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

In this tutorial, we will explore how to apply silhouette effects to images using the `SkiaShadersMask` class in Flutter. Silhouette effects can be used creatively to give images a unique and artistic appearance. We will use the `flutter_svg` package to load SVG images and the `skia_flutter` package to apply the silhouette effect.

## Table of Contents
- [Installing Required Packages](#installing-required-packages)
- [Loading SVG Images](#loading-svg-images)
- [Applying Silhouette Effect](#applying-silhouette-effect)
- [Conclusion](#conclusion)

## Installing Required Packages

To get started, we need to add the following dependencies to the `pubspec.yaml` file.

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_svg: ^0.22.0
  skia_flutter: ^0.1.0
```
Make sure to run `flutter pub get` to fetch the newly added packages.

## Loading SVG Images

Next, let's load an SVG image using the `flutter_svg` package. You can place the SVG file in the `assets` directory of your Flutter project.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_svg/flutter_svg.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Silhouette Effects'),
        ),
        body: Center(
          child: SvgPicture.asset(
            'assets/image.svg',
            height: 200,
            width: 200,
          ),
        ),
      ),
    );
  }
}
```

Make sure to replace `'assets/image.svg'` with the actual path to your SVG file.

## Applying Silhouette Effect

Now, let's apply the silhouette effect to the loaded SVG image using the `SkiaShadersMask` class from the `skia_flutter` package.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_svg/flutter_svg.dart';
import 'package:skia_flutter/skia_flutter.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Silhouette Effects'),
        ),
        body: Center(
          child: SkiaShaderMask(
            child: SvgPicture.asset(
              'assets/image.svg',
              height: 200,
              width: 200,
            ),
            shader: SkiaShadersMask.silhouette(),
          ),
        ),
      ),
    );
  }
}
```

We wrap the `SvgPicture.asset` widget with a `SkiaShaderMask` widget and provide the `SkiaShadersMask.silhouette()` shader to achieve the silhouette effect.

## Conclusion

In this tutorial, we explored how to apply silhouette effects to images using the `SkiaShadersMask` class in Flutter. Silhouette effects can be used to add an artistic touch to your UI and create visually appealing designs. Experiment with different SVG images and customize the silhouette effect to suit your requirements.

#flutter #silhouette-effect