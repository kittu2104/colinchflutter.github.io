---
layout: post
title: "Applying light leak effects with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

A light leak effect can add an artistic touch to your images or create a vintage look. In this tutorial, we will explore how to apply light leak effects using the `SkiaShadersMask` class in Flutter.

## Table of Contents
1. Introduction
2. Prerequisites
3. Setting up the project
4. Implementing the light leak effect
5. Conclusion

## 1. Introduction

Light leaks are accidental light exposures that create colorful or hazy effects in photographs. By replicating these effects, you can enhance the visual appeal of your Flutter applications. 

## 2. Prerequisites

To follow along with this tutorial, you'll need:

- Flutter SDK installed on your machine
- An IDE such as VS Code or Android Studio

## 3. Setting up the project

1. Create a new Flutter project by running the following command in your terminal:

    ```bash
    flutter create light_leak_project
    ```

2. Open the project in your preferred IDE.

3. Replace the contents of the `lib/main.dart` file with the following code:

    ```dart
    import 'package:flutter/material.dart';
    import 'dart:ui' as ui;
    
    void main() {
      runApp(MyApp());
    }
    
    class MyApp extends StatelessWidget {
      @override
      Widget build(BuildContext context) {
        return MaterialApp(
          title: 'Light Leak Effect',
          theme: ThemeData(
            primarySwatch: Colors.blue,
          ),
          home: MyHomePage(),
        );
      }
    }
    
    class MyHomePage extends StatelessWidget {
      @override
      Widget build(BuildContext context) {
        return Scaffold(
          appBar: AppBar(
            title: Text('Light Leak Effect'),
          ),
          body: Center(
            child: Container(
              width: 300,
              height: 300,
              child: CustomPaint(
                painter: LightLeakPainter(),
              ),
            ),
          ),
        );
      }
    }
    
    class LightLeakPainter extends CustomPainter {
      @override
      void paint(ui.Canvas canvas, ui.Size size) {
        // Apply light leak effect here using SkiaShadersMask
      }
    
      @override
      bool shouldRepaint(covariant CustomPainter oldDelegate) {
        return false;
      }
    }
    ```

## 4. Implementing the light leak effect

To apply the light leak effect, we will use the `SkiaShadersMask` class provided by the `dart:ui` package. This class allows us to mask our canvas with a shader, in this case, a gradient that simulates the light leak effect.

1. Add the following dependency to your project's `pubspec.yaml` file:

    ```yaml
    dependencies:
      flutter:
        sdk: flutter
      cupertino_icons: ^1.0.2
    ```

2. Run the following command in your terminal to update the project dependencies:

    ```bash
    flutter pub get
    ```

3. Replace the contents of the `LightLeakPainter` class's `paint` method with the following code:

    ```dart
    @override
    void paint(ui.Canvas canvas, ui.Size size) {
      final rect = Offset.zero & size;
    
      final gradient = ui.Gradient.radial(
        rect.center,
        rect.shortestSide / 2,
        [
          const Color(0xFF006633),
          const Color(0xFF00FF00),
          const Color(0xFF0099FF),
          const Color(0xFF9900FF),
        ],
        [0.0, 0.4, 0.6, 1.0],
        ui.TileMode.repeated,
      );
    
      final shaderMask = ui.MaskFilter.blur(
        ui.BlurStyle.outer,
        ui.BlurStyle.outer.convertRadiusToSigma(50),
      );
    
      final paint = ui.Paint()
        ..shader = gradient.createShader(rect)
        ..maskFilter = shaderMask;
    
      canvas.drawRect(rect, paint);
    }
    ```

4. Hot reload the application to see the light leak effect applied to the container.

## 5. Conclusion

By utilizing the `SkiaShadersMask` class in Flutter, you can easily add light leak effects to enhance the visual aesthetics of your applications. Experiment with different gradient colors and positions to achieve the desired artistic effects. Happy coding!

\#Flutter \#LightLeakEffect