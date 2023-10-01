---
layout: post
title: "useAnimatedWidgetTween hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: [FlutterHooks, AnimationInFlutter]
comments: true
share: true
---

Flutter Hooks is a powerful package that provides a set of reusable hooks to create robust and efficient Flutter applications. One of the useful hooks provided by Flutter Hooks is `useAnimatedWidgetTween`. In this blog post, we'll explore how to leverage this hook to create smooth and interactive animations in Flutter.

## What is `useAnimatedWidgetTween`?

`useAnimatedWidgetTween` is a hook provided by the Flutter Hooks package that simplifies the process of creating animated widgets in Flutter. It uses a combination of `AnimationController` and `Tween` to create smooth and dynamic transitions between different widget states.

## Getting Started

Before we dive into using `useAnimatedWidgetTween`, make sure you have the latest version of the Flutter Hooks package installed in your project. Open your `pubspec.yaml` file and add the following line under dependencies:

```dart
dependencies:
  flutter_hooks: ^0.20.0
```

Then, run `flutter pub get` to fetch the latest version of the package.

## Example Usage

To showcase the usage of `useAnimatedWidgetTween`, let's create a simple example where we animate the size of a container widget. Here's an example code snippet:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_hooks/flutter_hooks.dart';

class AnimatedContainerExample extends HookWidget {
  final AnimationController _controller;
  final Animation<double> _animation;

  AnimatedContainerExample()
      : _controller = useAnimationController(duration: Duration(seconds: 1)),
        _animation = useAnimateDouble(
          initialValue: 0.0,
          targetValue: 200.0,
          controller: _controller,
          curve: Curves.easeInOut,
          duration: Duration(seconds: 1),
        );

  @override
  Widget build(BuildContext context) {
    return AnimatedBuilder(
      animation: _controller,
      builder: (BuildContext context, Widget child) {
        return Container(
          width: _animation.value,
          height: _animation.value,
          color: Colors.blue,
        );
      },
    );
  }
}

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      body: Center(
        child: AnimatedContainerExample(),
      ),
    ),
  ));
}
```

In the above example, we define an `AnimatedContainerExample` widget that utilizes the `useAnimatedWidgetTween` hook to animate the size of a container. We initialize an `AnimationController` using the `useAnimationController` hook, which gives us a controller to drive our animation. Then, we define an `Animation<double>` using the `useAnimateDouble` hook, which creates a tween to animate the size based on the controller's value.

Inside the `build` method, we use the `AnimatedBuilder` widget to rebuild the container whenever the animation's value changes. The container's width and height are set based on the animation value, creating a smooth transition between the sizes.

## Conclusion

`useAnimatedWidgetTween` is a handy hook provided by the Flutter Hooks package that simplifies the process of creating animated widgets in Flutter. By leveraging this hook, you can easily create smooth and interactive animations to bring life to your Flutter applications.

*Tags: #FlutterHooks #AnimationInFlutter*