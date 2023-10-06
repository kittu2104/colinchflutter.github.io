---
layout: post
title: "Creating neon effects with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

Neon effects can add a vibrant and eye-catching look to your Flutter applications. With the SkiaShadersMask widget in Flutter, you can easily create neon effects by combining a colorful gradient with a mask. In this tutorial, we will explore how to create neon effects using SkiaShadersMask in Flutter.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Setting up the Project](#setting-up-the-project)
- [Implementing the Neon Effect](#implementing-the-neon-effect)
- [Conclusion](#conclusion)

## Prerequisites
Before getting started, make sure you have the following prerequisites:
- Flutter SDK installed on your machine
- A code editor of your choice (e.g., Visual Studio Code)

## Setting up the Project
To begin, create a new Flutter project by running the following command in your terminal:

```
flutter create neon_effects
cd neon_effects
```

Once the project is created, open it in your code editor.

## Implementing the Neon Effect
In Flutter, you can create custom effects using SkiaShadersMask. First, add the `skia` package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  skia: ^0.15.0  # Add this line
```

Next, run the following command to fetch the dependencies:

```
flutter pub get
```

Now, let's create a new Dart file named `neon_effect.dart`.

```dart
import 'package:flutter/material.dart';
import 'package:skia/shaders.dart' as shaders;

class NeonEffect extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Neon Effect'),
      ),
      body: Center(
        child: Container(
          width: 200,
          height: 200,
          decoration: BoxDecoration(
            borderRadius: BorderRadius.circular(100),
            color: Colors.black,
            boxShadow: [
              BoxShadow(
                color: Colors.green, // Neon color
                blurRadius: 10,
                spreadRadius: 0,
              ),
            ],
          ),
          child: ClipRRect(
            borderRadius: BorderRadius.circular(100),
            child: ShaderMask(
              shaderCallback: (Rect bounds) {
                return shaders.MaskShader(
                  shaders.LinearGradient(
                    colors: [Colors.transparent, Colors.white],
                
                    // Add more colors to customize the neon effect
                    stops: [0.5, 0.7],
                    tileMode: TileMode.mirror,
                  ).createShader(bounds),
                  TextDirection.ltr,
                );
              },
              child: Container(
                color: Colors.black,
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```

In the above code, we create a `NeonEffect` widget that displays a neon effect. We use `BoxDecoration` to create the neon glow effect with a `BoxShadow` and a circular shape. Inside the `ShaderMask`, we define a `shaderCallback` that creates a `MaskShader` using a gradient (`LinearGradient`). We can customize the neon effect by adding more colors and adjusting the stops.

To use the `NeonEffect` widget, modify the `lib/main.dart` file as follows:

```dart
import 'package:flutter/material.dart';
import 'package:neon_effects/neon_effect.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Neon Effects',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: NeonEffect(), // Change this line
    );
  }
}
```

Save your changes and run the app using the following command:

```
flutter run
```

You should now see a circular container with a neon glow effect on a black background.

## Conclusion
In this tutorial, we explored how to create neon effects using the SkiaShadersMask widget in Flutter. By combining a gradient with a mask, we can easily add attractive neon effects to our Flutter applications. Feel free to customize the colors and stops to create your own unique neon effects. Happy coding!

#flutter #neoneffects