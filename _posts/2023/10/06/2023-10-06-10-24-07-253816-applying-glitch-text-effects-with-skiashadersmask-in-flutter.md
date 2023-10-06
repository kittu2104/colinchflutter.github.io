---
layout: post
title: "Applying glitch text effects with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

Glitch text effects can add a creative and dynamic element to your Flutter application. Utilizing the `SkiaShadersMask` class from the Flutter `skia` package, you can easily apply glitch effects to text in your app.

In this tutorial, I will guide you through the steps to apply glitch text effects using `SkiaShadersMask` in Flutter.

## Table of Contents
- [Setting up the project](#setting-up-the-project)
- [Applying glitch text effects](#applying-glitch-text-effects)
- [Conclusion](#conclusion)

<a id="setting-up-the-project"></a>
## Setting up the project

To get started, create a new Flutter project and open it in your favorite code editor.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Glitch Text Effects',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: GlitchTextPage(),
    );
  }
}

class GlitchTextPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Glitch Text Effects'),
      ),
      body: Center(
        child: Text(
          'Hello, Flutter!',
          style: TextStyle(
            fontSize: 36,
            fontWeight: FontWeight.bold,
          ),
        ),
      ),
    );
  }
}
```

<a id="applying-glitch-text-effects"></a>
## Applying glitch text effects

To apply glitch text effects, we will use the `SkiaShadersMask` class provided by the `skia` package. This class lets us apply a mask to the text and create a glitch effect.

First, let's add the `skia` package dependency to our `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  skia: ^0.7.0
```

Next, we will modify the `GlitchTextPage` widget to apply the glitch effect. Wrap the `Text` widget with a `ShaderMask` widget and provide a `SkiaShadersMask` as the value of the `shaderCallback` parameter:

```dart
import 'package:skia/skia.dart' as skia;

class GlitchTextPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Glitch Text Effects'),
      ),
      body: Center(
        child: ShaderMask(
          shaderCallback: (Rect bounds) {
            return skia.SkiaShadersMask(
              textSpan: TextSpan(
                text: 'Hello, Flutter!',
                style: TextStyle(
                  fontSize: 36,
                  fontWeight: FontWeight.bold,
                ),
              ),
              shader: skia.GlitchShader(
                color1: Colors.blue,
                color2: Colors.green,
              ),
              mode: skia.BlendMode.srcIn,
            ).createShader(bounds);
          },
          child: Text(
            'Hello, Flutter!',
            style: TextStyle(
              fontSize: 36,
              fontWeight: FontWeight.bold,
            ),
          ),
        ),
      ),
    );
  }
}
```

In the code above, we create a `SkiaShadersMask` instance and pass the `TextSpan` representing the text that we want to apply the effect on. We then provide a `GlitchShader` to the `SkiaShadersMask` instance, specifying the glitch effect colors. Finally, we create the shader by calling `createShader(bounds)` on the `SkiaShadersMask` instance, and use it as the `shaderCallback` value of the `ShaderMask` widget.

Run your app, and you should see the glitch effect applied to the text.

<a id="conclusion"></a>
## Conclusion

In this tutorial, you learned how to apply glitch text effects using `SkiaShadersMask` in Flutter. By leveraging the `skia` package and the `GlitchShader` provided by `SkiaShadersMask`, you can easily add dynamic and visually engaging glitch effects to your text elements in Flutter applications.

Remember to experiment with different colors and parameters to achieve your desired glitch effect. Happy coding!

##### #Flutter #GlitchTextEffects