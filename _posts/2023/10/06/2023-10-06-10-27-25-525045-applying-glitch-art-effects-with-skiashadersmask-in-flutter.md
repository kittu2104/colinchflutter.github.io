---
layout: post
title: "Applying glitch art effects with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

In this article, we will explore how to apply glitch art effects to images in a Flutter application using the SkiaShadersMask package. Glitch art refers to intentionally distorting digital images to create visually striking and unique effects.

## Prerequisites

Before we begin, ensure that you have Flutter installed on your machine. You can download and install Flutter from the official Flutter website.

Also, make sure you have created a new Flutter project or have an existing project you can work with.

## Installing SkiaShadersMask

To get started, open your project's `pubspec.yaml` file and add the following dependency:

```dart
dependencies:
  skia_shaders_mask: ^0.0.1
```

Save the file and run `flutter pub get` to fetch the package.

## Applying the Glitch Effect

Once the package is installed, we can start applying the glitch effect to our images.

Import the necessary packages in your Dart file:

```dart
import 'package:flutter/material.dart';
import 'package:skia_shaders_mask/skia_shaders_mask.dart';
```

Next, create a custom widget that extends `StatefulWidget`:

```dart
class GlitchArtWidget extends StatefulWidget {
  @override
  _GlitchArtWidgetState createState() => _GlitchArtWidgetState();
}
```

Inside the state class, declare a `MaskFilter` object:

```dart
class _GlitchArtWidgetState extends State<GlitchArtWidget> {
  MaskFilter _maskFilter;

  @override
  void initState() {
    super.initState();
    _createMaskFilter();
  }

  void _createMaskFilter() {
    // Create the mask filter here
    // You can play around with parameters to get different glitch effects
    _maskFilter = SkiaShadersMask.glitch(
      child: const Image(
        image: AssetImage("assets/my_image.jpg"),
      ),
      seed: 42,
      intensity: 0.5,
      blockCount: 50,
    );
  }

  @override
  Widget build(BuildContext context) {
    return Center(
      child: ShaderMask(
        shaderCallback: (bounds) => _maskFilter,
        child: const Image(
          image: AssetImage("assets/my_image.jpg"),
        ),
      ),
    );
  }
}
```

Here, we use the `SkiaShadersMask.glitch()` method to create a `MaskFilter` with glitch art effects. You can adjust the `seed`, `intensity`, and `blockCount` parameters to customize the effect.

Inside the `build()` method, we wrap the `Image` widget with a `ShaderMask` widget and pass `_maskFilter` as the `shaderCallback`.

Finally, use the `GlitchArtWidget` in your application's UI:

```dart
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Glitch Art',
      home: Scaffold(
        appBar: AppBar(
          title: const Text('Glitch Art'),
        ),
        body: GlitchArtWidget(),
      ),
    );
  }
}
```

That's it! When you run your Flutter application, you should see the glitch art effect applied to the image.

## Conclusion

In this tutorial, we learned how to apply glitch art effects to images in a Flutter application using the SkiaShadersMask package. Experiment with different parameters to achieve various glitch art effects and create stunning visuals in your app.

Remember to check out the official package documentation for more details and options: [SkiaShadersMask](https://pub.dev/packages/skia_shaders_mask).

Happy glitching! 🎨

#flutter #glitchart