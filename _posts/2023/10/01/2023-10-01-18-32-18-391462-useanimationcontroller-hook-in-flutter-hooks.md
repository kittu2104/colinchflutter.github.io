---
layout: post
title: "useAnimationController hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: [FlutterHooks]
comments: true
share: true
---

Flutter Hooks is a powerful package that enhances the state management capabilities of Flutter applications. One of the most useful hooks provided by the package is `useAnimationController`, which allows you to easily create and control animations in your Flutter app. In this blog post, we will explore how to use the `useAnimationController` hook to create smooth and interactive animations.

## Installation

Before we can start using the `useAnimationController` hook, we need to install the Flutter Hooks package. Open your pubspec.yaml file and add the following dependency:

```dart
dependencies:
  flutter_hooks: ^0.18.0
```

Then, run `flutter pub get` to fetch the package.

## Getting Started

To start using the `useAnimationController` hook, we need to import the required packages:

```dart
import 'package:flutter_hooks/flutter_hooks.dart';
import 'package:flutter/material.dart';
```

## Creating an Animation Controller

Next, let's create an animation controller using the `useAnimationController` hook. The `useAnimationController` hook takes an optional `duration` parameter, which specifies the duration of the animation. By default, the duration is set to 300 milliseconds.

```dart
Widget MyAnimatedWidget() {
  final animationController = useAnimationController(
    duration: Duration(milliseconds: 500),
  );
  
  // Rest of the widget implementation
}
```

## Controlling the Animation

With the animation controller in place, we can now control the animation by manipulating its properties. For example, to start the animation, we can call the `forward` method:

```dart
animationController.forward();
```

To reverse the animation, simply call the `reverse` method:

```dart
animationController.reverse();
```

To pause or resume the animation, use the `animateTo` method:

```dart
animationController.animateTo(0.5); // pause at half progress
animationController.animateTo(1.0); // resume full progress
```

## Animating Widgets

To animate widgets based on the animation controller's progress, we can use the `HookBuilder` widget provided by Flutter Hooks. The `HookBuilder` widget automatically rebuilds itself whenever any of its hooks change.

```dart
Widget MyAnimatedWidget() {
  final animationController = useAnimationController();

  return HookBuilder(
    builder: (context) {
      final progress = useAnimation(animationController);

      return Container(
        width: 200 * progress, // animate width
        height: 200 * progress, // animate height
        color: Colors.blue,
      );
    },
  );
}
```

## Conclusion

Using the `useAnimationController` hook in Flutter Hooks makes it easy to create and control animations in your Flutter applications. By integrating this hook into your code, you can develop smooth and interactive animations with minimal effort. Start using Flutter Hooks and take your app's animation capabilities to the next level.

## #Flutter #FlutterHooks