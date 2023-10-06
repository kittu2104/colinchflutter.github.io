---
layout: post
title: "Applying distortion effects with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

In this tutorial, we will explore how to apply distortion effects using SkiaShadersMask in Flutter. Skia is a 2D graphics library used by Flutter, and SkiaShadersMask is a class that allows us to create custom shaders to apply various effects to our UI.

## Table of Contents
1. [Setting up the project](#setting-up-the-project)
2. [Creating the custom shader](#creating-the-custom-shader)
3. [Applying the shader to a widget](#applying-the-shader-to-a-widget)
4. [Conclusion](#conclusion)

Let's dive into the process step-by-step.

## 1. Setting up the project<a name="setting-up-the-project"></a>

Before we begin, make sure you have Flutter installed on your machine. If not, head over to the [Flutter installation guide](https://flutter.dev/docs/get-started/install) and follow the instructions.

Create a new Flutter project and open it in your preferred code editor:

```bash
flutter create distortion_app
cd distortion_app
```

## 2. Creating the custom shader<a name="creating-the-custom-shader"></a>

To create the custom shader, we'll be using the `Skia` package. Add the `skia` dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
  skia:
```

Run `flutter pub get` to fetch the package.

Next, create a file named `distortion_shader.dart`. In this file, add the following code to define the custom shader:

```dart
import 'package:skia/skia.dart';

class DistortionShader extends Shader {
  final Float32List matrix;

  DistortionShader(this.matrix)
      : super(
          Point<int>(0, 0),
          Point<int>(0, 0),
          Float32List.fromList([0, 0, 0, 0]),
          false,
        );

  @override
  ShaderType get shaderType => ShaderType.Color;
}
```

In the `DistortionShader` class, we extend the `Shader` class from the `skia` package. The constructor takes a `Float32List` parameter called `matrix`, which will be used to apply the distortion effect. We override the `shaderType` getter to specify that this is a color shader.

## 3. Applying the shader to a widget<a name="applying-the-shader-to-a-widget"></a>

Now that we have our custom shader, let's apply it to a widget. For demonstration purposes, we'll apply the distortion effect to a `Container` widget.

Open the `lib/main.dart` file and replace the existing content with the following code:

```dart
import 'package:flutter/material.dart';
import 'dart:typed_data';
import 'distortion_shader.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final distortionMatrix = Float32List.fromList([1.0, 0.0, 0.0, 1.0]);
    final shader = DistortionShader(distortionMatrix);

    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Distortion App'),
        ),
        body: Center(
          child: Container(
            width: 200,
            height: 200,
            decoration: BoxDecoration(
              color: Colors.blue,
              image: DecorationImage(
                image: NetworkImage(
                  'https://example.com/image.jpg',
                ),
                colorFilter: ColorFilter.linearToSrgbGamma(),
                shader: shader,
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```

In this code, we create an instance of the `DistortionShader` class and pass a `Float32List` called `distortionMatrix` with default values. We then use this `shader` object in the `Container` widget's `DecorationImage` to apply the distortion effect.

Make sure to replace the image URL in the `NetworkImage` widget with the desired image URL.

## 4. Conclusion<a name="conclusion"></a>

By using SkiaShadersMask in Flutter, we can easily apply distortion effects to our UI. In this tutorial, we covered the basic steps of setting up a project, creating a custom shader, and applying it to a widget.

Feel free to experiment with different distortion matrices to achieve unique effects. Remember to check the Skia documentation for more advanced techniques and options.

Now go ahead and have fun creating amazing distortion effects in your Flutter apps! 🎉🚀

#flutter #skia