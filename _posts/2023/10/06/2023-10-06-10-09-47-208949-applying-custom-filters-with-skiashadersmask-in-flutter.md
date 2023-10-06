---
layout: post
title: "Applying custom filters with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

In Flutter, you can apply various built-in filters to your UI elements to enhance their visual appearance. However, there may be cases where you need to apply a custom filter to achieve a specific effect. This is where the `SkiaShadersMask` class comes into play. 

The `SkiaShadersMask` class allows you to create and apply custom pixel shaders to your UI elements in Flutter. It's based on Skia, the graphics engine used in Flutter, and provides a powerful way to manipulate the appearance of your UI elements.

## Getting Started

To get started, make sure you have Flutter installed on your system. You can install Flutter by following the official Flutter documentation.

Once you have Flutter installed, create a new Flutter project and navigate to its root directory in your command line or terminal.

## Adding Dependencies

To use `SkiaShadersMask`, you need to add the `flutter_skia` package as a dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  # other dependencies
  flutter_skia: ^0.1.0
```

After adding the dependency, run `flutter pub get` to fetch the package.

## Applying a Custom Filter

To apply a custom filter using `SkiaShadersMask`, you'll need to wrap your UI element in a `ShaderMask` widget. The `ShaderMask` widget takes a `BlendMode` and a `Shader` as parameters.

Here's an example of how to apply a custom filter with `SkiaShadersMask`:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_skia/flutter_skia.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // Custom shader
    final customShader = skia.Shader.makeLinearGradient(
      <skia.Color>[
        skia.Color.fromColor(Colors.red),
        skia.Color.fromColor(Colors.blue),
      ],
    );

    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Custom Filter'),
        ),
        body: Center(
          child: ShaderMask(
            shaderCallback: (rect) {
              final paint = skia.Paint()..shader = customShader;
              return paint;
            },
            child: Container(
              width: 200,
              height: 200,
              color: Colors.green,
            ),
          ),
        ),
      ),
    );
  }
}
```

In this example, we define a custom shader using `skia.Shader.makeLinearGradient` and pass it to the `shaderCallback` of the `ShaderMask` widget. The `shaderCallback` is responsible for creating the shader to be applied to the UI element.

The `ShaderMask` widget wraps a `Container` widget, which represents the UI element we want to apply the custom filter to. In this case, we set the color of the container to green.

After running the code, you should see a square container with a gradient fill transitioning from red to blue, applied as a custom filter.

## Conclusion

By using the `SkiaShadersMask` class in Flutter, you can apply custom filters to your UI elements and achieve unique visual effects. The example above demonstrates how to apply a custom gradient filter, but you can explore other shaders and effects offered by Skia to create even more impressive visuals in your Flutter applications.

Remember to experiment, iterate, and have fun while exploring the possibilities of Skia and `SkiaShadersMask`. Happy coding!

#flutter #SkiaShadersMask