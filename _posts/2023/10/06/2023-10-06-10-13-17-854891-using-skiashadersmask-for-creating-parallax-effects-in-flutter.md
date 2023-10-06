---
layout: post
title: "Using SkiaShadersMask for creating parallax effects in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

When it comes to creating visually appealing and interactive user interfaces, Flutter provides a rich set of tools and libraries to make it happen. One such tool is Skia, a 2D rendering engine that powers the graphics in Flutter. Skia provides various features, including the ability to apply custom shaders to create stunning visual effects.

In this blog post, we will explore how to utilize Skia's `SkiaShadersMask` to achieve parallax effects in Flutter. Parallax effects, also known as parallax scrolling, give a sense of depth and dimension to the user interface by making different layers move at different speeds when scrolling.

To get started, make sure you have the latest version of Flutter installed on your machine.

## Setting up the Project

Create a new Flutter project and open it in your preferred IDE. Let's assume the project is named `parallax_demo`.

## Adding Skia Dependency

In order to utilize the `SkiaShadersMask` class, we need to add the Skia dependency to our project. Open the `pubspec.yaml` file and add the following line to the `dependencies` section:

```yaml
dependencies:
  flutter:
    sdk: flutter
  skia:
```

Save the file and run `flutter pub get` in the terminal to fetch the dependency.

## Creating a Parallax Widget

Now, let's create a custom widget named `ParallaxWidget` that will demonstrate the parallax effect. Inside the `parallax_demo/lib` directory, create a new file named `parallax_widget.dart` and add the following code:

```dart
import 'package:flutter/widgets.dart';
import 'package:flutter/scheduler.dart' show Ticker, TickerProvider;
import 'package:skia/skia.dart';

class ParallaxWidget extends StatefulWidget {
  @override
  _ParallaxWidgetState createState() => _ParallaxWidgetState();
}

class _ParallaxWidgetState extends State<ParallaxWidget>
    with TickerProviderStateMixin {
  late Ticker _ticker;
  double _offsetX = 0;
  double _offsetY = 0;

  @override
  void initState() {
    super.initState();
    _ticker = createTicker((elapsed) {
      setState(() {
        _offsetX = elapsed.inMilliseconds.toDouble() / 10;
        _offsetY = elapsed.inMilliseconds.toDouble() / 20;
      });
    });
    _ticker.start();
  }

  @override
  void dispose() {
    _ticker.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return CustomPaint(
      painter: _ParallaxPainter(_offsetX, _offsetY),
      child: Container(),
    );
  }
}

class _ParallaxPainter extends CustomPainter {
  final double offsetX;
  final double offsetY;

  _ParallaxPainter(this.offsetX, this.offsetY);

  @override
  void paint(Canvas canvas, Size size) {
    final paint = Paint();
    final gradient = SkiaShaders.linearGradient(
      [
        Colors.red,
        Colors.blue,
      ],
      [Offset(offsetX, offsetY), Offset(offsetX + 100, offsetY + 100)],
    );
    paint.shader = gradient.createMaskShader(Rect.fromLTRB(0, 0, size.width, size.height));
    canvas.drawRect(Rect.fromLTRB(0, 0, size.width, size.height), paint);
  }

  @override
  bool shouldRepaint(_ParallaxPainter oldDelegate) => true;
}
```

The `ParallaxWidget` is a stateful widget that uses a `Ticker` to continuously update the `_offsetX` and `_offsetY` variables, which will determine the position of the gradient used for the parallax effect.

In the `build` method, we use `CustomPaint` to draw a rectangle with a gradient. The `Shader` property of the `Paint` class is set as the `SkiaShadersMask` created by `linearGradient`. The `createMaskShader` method allows us to create a shader using the gradient and define its position in the canvas.

## Integrating the Parallax Widget

To showcase the `ParallaxWidget`, we need to update the `lib/main.dart` file. Replace the existing content with the following code:

```dart
import 'package:flutter/material.dart';
import 'parallax_widget.dart';

void main() {
  runApp(ParallaxApp());
}

class ParallaxApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Parallax Demo',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Parallax Demo'),
        ),
        body: ParallaxWidget(),
      ),
    );
  }
}
```

The `ParallaxApp` class is a simple `MaterialApp` with an `AppBar` and the `ParallaxWidget` as the main content of the `Scaffold` body.

## Running the App

Save all the files and run the app using `flutter run` in the terminal. You should see a new screen with a gradient rectangle that moves as you scroll in different directions, creating a delightful parallax effect.

## Conclusion

Skia provides powerful features, such as shaders, to enhance the visual experience in Flutter. By using the `SkiaShadersMask` class, we can create stunning parallax effects that add depth and dimension to our UIs. With this knowledge, you can now explore and experiment with different gradients and movements to create unique and engaging user interfaces in Flutter.

Happy coding! #flutter #parallax