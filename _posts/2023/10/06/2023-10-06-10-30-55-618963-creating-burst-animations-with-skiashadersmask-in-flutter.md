---
layout: post
title: "Creating burst animations with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

In this tutorial, we'll explore how to create burst animations using SkiaShadersMask in Flutter. Burst animations are a great way to add dynamic and eye-catching effects to your Flutter app, and SkiaShadersMask provides the necessary tools to achieve this.

## Table of Contents
- Introduction
- Setting up the Project
- Creating Burst Animation
- Conclusion
- Hashtags: #Flutter #Animation

## Introduction

Burst animations involve the creation of multiple particles that rapidly expand and fade out, creating a burst effect. These animations are commonly used in games, loading screens, or to draw attention to certain elements in your app.

To achieve burst animations in Flutter, we'll utilize the SkiaShadersMask package, which provides a custom shader-based animation with high performance and flexibility.

## Setting up the Project

Before we begin, make sure you have Flutter installed on your machine. Create a new Flutter project and open it in your favorite code editor.

First, add the `flutter_skia_shaders_mask` package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  
  flutter_skia_shaders_mask: ^0.1.0
```

Import the necessary packages in your Dart file:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_skia_shaders_mask/flutter_skia_shaders_mask.dart';
```

## Creating Burst Animation

To create a burst animation, we'll use a `SkiaShadersMask` widget, which applies a shader mask effect to its child widget.

```dart
class BurstAnimation extends StatefulWidget {
  @override
  _BurstAnimationState createState() => _BurstAnimationState();
}

class _BurstAnimationState extends State<BurstAnimation>
    with SingleTickerProviderStateMixin {
  AnimationController _controller;
  Animation<double> _animation;

  @override
  void initState() {
    _controller = AnimationController(
      duration: Duration(milliseconds: 1000),
      vsync: this,
    );

    _animation = Tween<double>(begin: 0, end: 1).animate(_controller);

    _controller.forward();
    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Burst Animation'),
      ),
      body: Center(
        child: SkiaShadersMask(
          maskTileMode: TileMode.clamp,
          maskShader: FlutterSkiaShaders.createBurstShader(),
          child: Container(
            width: 200,
            height: 200,
          ),
        ),
      ),
    );
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }
}
```

In the above code, we create a `BurstAnimation` widget that extends `StatefulWidget`. Inside the widget, we define an `AnimationController` and an `Animation` to control the burst animation. The `initState` method initializes the animation and starts it by calling `_controller.forward()`.

In the `build` method, we use a `SkiaShadersMask` widget as our root widget, applying the `FlutterSkiaShaders.createBurstShader()` as the mask shader. The `maskTileMode` property determines how the mask should be repeated, and the `child` is the container that will be masked with the burst effect.

## Conclusion

In this tutorial, we explored how to create burst animations using SkiaShadersMask in Flutter. Burst animations can add an engaging and dynamic element to your app, making it more visually appealing. Experiment with different mask shaders and animation controllers to customize your burst animations further.

Remember to import the necessary packages and set up the animation controller and animation. Then, apply the SkiaShadersMask widget as the root widget, using a specific mask shader to achieve the desired burst effect.

Have fun creating burst animations and enhancing your Flutter app!

Hashtags: #Flutter #Animation