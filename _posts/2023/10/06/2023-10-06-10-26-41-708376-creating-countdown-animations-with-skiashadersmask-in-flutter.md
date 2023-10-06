---
layout: post
title: "Creating countdown animations with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

In this tutorial, we will explore how to create countdown animations using the SkiaShadersMask widget in Flutter. Countdown animations are a great way to add a visual element to your app and provide a sense of urgency or anticipation. We will be using Flutter's powerful rendering engine, Skia, along with the SkiaShadersMask widget to achieve this effect.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Setting up the project](#setting-up-the-project)
- [Creating the countdown animation](#creating-the-countdown-animation)
- [Conclusion](#conclusion)

## Prerequisites

Before we begin, ensure that you have Flutter installed on your machine. You can install Flutter by following the official [installation guide](https://flutter.dev/docs/get-started/install).

## Setting up the project

Let's start by creating a new Flutter project. Open your terminal or command prompt and execute the following command:

```shell
flutter create countdown_animation
```

Once the project is created, navigate into the project directory:

```shell
cd countdown_animation
```

Open the project in your favourite text editor or IDE.

## Creating the countdown animation

To create the countdown animation, we will use the SkiaShadersMask widget provided by the `flutter_shaders_mask` package. Add the package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  
  flutter_shaders_mask: ^1.0.0
```

Run `flutter pub get` to fetch the package.

Next, create a new Dart file called `countdown_animation.dart` in the `lib` folder and replace the default code with the following:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_shaders_mask/flutter_shaders_mask.dart';

class CountdownAnimation extends StatefulWidget {
  @override
  _CountdownAnimationState createState() => _CountdownAnimationState();
}

class _CountdownAnimationState extends State<CountdownAnimation> with SingleTickerProviderStateMixin {
  AnimationController _controller;
  Animation<double> _animation;

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: Duration(seconds: 10),
      vsync: this,
    )..forward();

    _animation = CurvedAnimation(parent: _controller, curve: Curves.linear);
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Countdown Animation'),
      ),
      body: Center(
        child: SkiaShadersMask(
          child: AnimatedBuilder(
            animation: _animation,
            builder: (context, child) {
              return Container(
                width: 200,
                height: 200,
                color: Colors.blue,
                alignment: Alignment.center,
                child: Text(
                  '${_controller.duration * _controller.value ~/ 1}',
                  style: TextStyle(
                    fontSize: 60,
                    color: Colors.white,
                    fontWeight: FontWeight.bold,
                  ),
                ),
              );
            },
          ),
          shader: LinearGradient(
            colors: [
              Colors.transparent,
              Colors.black,
              Colors.black,
              Colors.transparent,
            ],
            stops: [0.0, 0.2, 0.8, 1.0],
          ).createShader,
        ),
      ),
    );
  }
}
```

In this code snippet, we create a stateful widget called `CountdownAnimation`. Inside the widget, we define an `AnimationController` and an `Animation<double>` to drive our countdown animation. The `SkiaShadersMask` widget wraps the child widget and applies a shader to create the countdown effect.

The `AnimationController` is responsible for managing the animation duration and progress. We pass the `Animation` to the `AnimatedBuilder` to rebuild the UI in response to animation updates. In this case, we update the text widget with the remaining time.

The `SkiaShadersMask` widget takes a child widget and a shader. We use a `LinearGradient` shader to create the fading effect for the countdown animation. The gradient goes from transparent to black, then back to transparent.

Save the file and open the `main.dart` file. Replace the default code with the following:

```dart
import 'package:flutter/material.dart';
import 'countdown_animation.dart';

void main() {
  runApp(CountdownApp());
}

class CountdownApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Countdown Animation',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: CountdownAnimation(),
      debugShowCheckedModeBanner: false,
    );
  }
}
```

In this code, we define a `main` function that runs the `CountdownApp` widget. The `CountdownApp` widget is a `MaterialApp` that sets our app's title, theme, and sets the `CountdownAnimation` as the home screen.

Now, run the app using the following command:

```shell
flutter run
```

You should see the countdown animation on your device or emulator.

## Conclusion

In this tutorial, we explored how to create countdown animations using the SkiaShadersMask widget in Flutter. We learned how to set up the project, create the countdown animation, and use the SkiaShadersMask widget to apply the fading effect. Countdown animations add a visually engaging element to your app and can be customized to fit your app's design. Explore different animation techniques and shader effects to create visually stunning countdown animations in your Flutter apps.

Feel free to experiment and customize the countdown animation according to your requirements. You can tweak the duration, colors, and styles to create unique countdown experiences. Enjoy animating with Flutter!

— #Flutter #CountdownAnimation