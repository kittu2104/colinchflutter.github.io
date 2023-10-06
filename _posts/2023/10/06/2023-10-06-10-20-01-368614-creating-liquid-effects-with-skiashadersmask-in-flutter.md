---
layout: post
title: "Creating liquid effects with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

In this tutorial, we will explore how to create liquid effects using the SkiaShadersMask class in Flutter. SkiaShadersMask is a powerful tool that allows you to apply custom shader effects to your Flutter widgets, enabling you to create stunning visual effects.

## Prerequisites

To follow along with this tutorial, you should have a basic understanding of Flutter and have Flutter SDK installed on your development machine.

## Setting up the Project

1. Create a new Flutter project by running the following command in your terminal:

   ```plaintext
   flutter create liquid_effects
   ```

2. Open the project in your preferred code editor.

## Adding Dependencies

To use the SkiaShadersMask class, you need to add the `flutter_svg` package to your `pubspec.yaml` file. Add the following line under the `dependencies` section:

```yaml
dependencies:
  flutter_svg: ^0.22.0
```

Save the file, and run the following command in your terminal to download the dependencies:

```plaintext
flutter pub get
```

## Creating a Liquid Effect

1. Open the `lib/main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_svg/flutter_svg.dart';

void main() {
  runApp(LiquidEffectsApp());
}

class LiquidEffectsApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Liquid Effects'),
        ),
        body: SafeArea(
          child: Center(
            child: Container(
              width: 200,
              height: 200,
              child: SkiaShadersMask(
                child: SvgPicture.asset(
                  'assets/liquid.svg',
                  semanticsLabel: 'Liquid Effect',
                ),
                shaderCallback: (Rect bounds) {
                  return LinearGradient(
                    colors: [Colors.red, Colors.blue],
                    stops: [0.0, 1.0],
                  ).createShader(bounds);
                },
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```

In this code snippet, we have defined a basic Flutter app with a centered container that holds a SkiaShadersMask widget. Inside the SkiaShadersMask widget, we have placed an SVG image using the SvgPicture.asset widget. The `shaderCallback` property of the SkiaShadersMask widget allows us to define a custom shader effect. In this example, we are using a LinearGradient shader that creates a gradient from red to blue.

2. Create a new directory called `assets` in the root of your project, and place an SVG file named `liquid.svg` in the assets directory. You can find sample SVG files for liquid effects on various platforms or create your own.

3. Open the `pubspec.yaml` file and add the following lines under the `flutter` section:

```yaml
flutter:
  assets:
    - assets/
```

These lines will ensure that the assets directory and its contents are included in your Flutter app when it is built.

## Running the App

To run the app, execute the following command in your terminal:

```plaintext
flutter run
```

If everything is set up correctly, you should see a liquid effect in a centered container on the app screen.

## Conclusion

In this tutorial, we explored how to create liquid effects using SkiaShadersMask in Flutter. This powerful tool provides endless possibilities for creating custom shader effects, allowing you to enhance the visual appeal of your Flutter apps. Experiment with different shader effects and unleash your creativity to create stunning visual experiences.

Follow us on Twitter for more Flutter tutorials and tips: [@exampletechblog](https://twitter.com/exampletechblog)

#flutter #liquideffects