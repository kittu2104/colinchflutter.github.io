---
layout: post
title: "useAnimatedPositionedTween hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: [flutter, flutterhooks]
comments: true
share: true
---

In Flutter Hooks, the `useAnimatedPositionedTween` hook is a powerful tool that allows you to create dynamic animations using `Positioned` widgets in a declarative way. This hook provides a simple and intuitive API to define animations that automatically update when dependencies change.

## Installation

Before using the `useAnimatedPositionedTween` hook, make sure you have the `flutter_hooks` package added to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_hooks: ^0.18.0
```

You can then run `flutter pub get` to fetch and update the package in your project.

## Usage

Here's an example of how to use the `useAnimatedPositionedTween` hook in Flutter Hooks:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_hooks/flutter_hooks.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends HookWidget {
  @override
  Widget build(BuildContext context) {
    final animationController = useAnimationController(duration: Duration(seconds: 1));
    final animation = useAnimatedPositionedTween(
      duration: Duration(seconds: 1),
      controller: animationController,
      begin: Offset.zero,
      end: Offset(200, 200),
      curve: Curves.easeInOut,
      child: Container(
        width: 100,
        height: 100,
        color: Colors.blue,
      ),
    );

    return MaterialApp(
      home: Scaffold(
        body: Center(
          child: GestureDetector(
            onTap: () {
              animationController.reset();
              animationController.forward();
            },
            child: animation,
          ),
        ),
      ),
    );
  }
}
```

In this example, we define an `animationController` using the `useAnimationController` hook to control the animation duration. We then define the `animation` using the `useAnimatedPositionedTween` hook, specifying the `begin` and `end` positions, `duration`, and `curve`.

The `animation` is wrapped around a `Container` widget, which will be animated from the `begin` position to the `end` position when tapping on the screen. The `animationController.reset()` is used to reset the animation to its initial position, and `animationController.forward()` is used to start the animation.

## Conclusion

The `useAnimatedPositionedTween` hook in Flutter Hooks provides a convenient way to create dynamic animations using `Positioned` widgets. It allows you to define animations that automatically update when dependencies change, making it easier to build interactive and visually appealing Flutter applications.

#flutter #flutterhooks