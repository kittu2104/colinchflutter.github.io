---
layout: post
title: "Applying motion effects with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

In Flutter, you can create visually engaging user interfaces by combining animations and graphics effects. One such effect is applying motion effects using the `SkiaShadersMask` class from the Flutter SDK.

The `SkiaShadersMask` allows you to apply a gradient-based motion effect to any UI element. This effect can give your app a dynamic and interactive feel, making it more visually appealing.

Let's see how we can apply a motion effect using the `SkiaShadersMask` class.

## Step 1: Add the dependency

To use the `SkiaShadersMask` class, you need to add the `flutter_skia` package to your Flutter project. Open your `pubspec.yaml` file and add the following dependency:

```
dependencies:
  flutter_skia: ^0.1.0
```

Then run `flutter pub get` to install the package.

## Step 2: Creating a Shader

To create a motion effect, we need to create a `Shader` object. The `Shader` defines the gradient and motion properties that we want to apply to our UI element.

Here's an example of creating a linear gradient `Shader` with motion effect:

```dart
import 'dart:ui';
import 'package:flutter/painting.dart';

final Shader motionShader = LinearGradient(
  begin: Alignment.topLeft,
  end: Alignment.bottomRight,
  colors: [Colors.red, Colors.blue],
).createShader(Rect.fromLTWH(0, 0, 200, 200));
```

In this example, we create a linear gradient `Shader` starting from the top left and ending at the bottom right. The gradient contains two colors: red and blue. The `Rect` defines the bounds of the shader.

## Step 3: Applying the Shader to an element

Once we have the `Shader` object, we can apply it to any UI element using the `SkiaShadersMask` widget.

Let's see an example of applying the `motionShader` to a `Container`:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_skia/flutter_skia.dart';

class MotionEffectExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return SkiaShadersMask(
      shader: motionShader,
      child: Container(
        width: 200,
        height: 200,
        color: Colors.white,
      ),
    );
  }
}
```

In this example, we wrap the `Container` widget with the `SkiaShadersMask` and pass the `motionShader` as the `shader` property. This will apply the motion effect to the `Container` widget.

## Conclusion

By using the `SkiaShadersMask` class in Flutter, you can easily apply motion effects to your UI elements. Experiment with different gradients and motion properties to create stunning visuals in your Flutter apps.

Now go ahead and add some motion effects to your Flutter app and make it more engaging!

#flutter #FlutterMotionEffects