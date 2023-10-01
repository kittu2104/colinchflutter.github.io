---
layout: post
title: "useAnimatedPhysicalModel hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: [FlutterHooks, AnimatedPhysicalModel]
comments: true
share: true
---

Flutter Hooks is a powerful and popular package for managing stateful logic in Flutter applications. It streamlines the process of building complex UIs and makes your code more readable and maintainable. In this blog post, we will dive into one of the most exciting features of Flutter Hooks - the `useAnimatedPhysicalModel` hook.

## What is `useAnimatedPhysicalModel`?

The `useAnimatedPhysicalModel` hook is a part of the `flutter_hooks` package and allows you to create animated physical models in your Flutter applications. It lets you define and control the visual representation of a physical shape along with its animation parameters, such as color, elevation, and shadow.

## How to use `useAnimatedPhysicalModel`?

To use the `useAnimatedPhysicalModel` hook, you need to follow these steps:

1. Install the `flutter_hooks` package through your `pubspec.yaml` file if you haven't already.
2. Import the required packages:
```dart
import 'package:flutter_hooks/flutter_hooks.dart';
import 'package:flutter/material.dart';
```
3. Create a stateful widget that encompasses your UI:
```dart
class MyAnimatedModelWidget extends HookWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: MyAnimatedPhysicalModel(),
      ),
    );
  }
}
```
4. Create a new class for your animated physical model, extending the `HookWidget`:
```dart
class MyAnimatedPhysicalModel extends HookWidget {
  @override
  Widget build(BuildContext context) {
    final elevation =  useAnimationController(
      initialValue: 0.0,
      lowerBound: 0.0,
      upperBound: 10.0,
      duration: Duration(seconds: 1),
    );

    final color = useAnimationController<Color>(
      initialValue: Colors.blue,
      duration: Duration(seconds: 1),
    );

    final shadowColor = useAnimationController<Color>(
      initialValue: Colors.black,
      duration: Duration(seconds: 1),
    );

    return GestureDetector(
      onTap: () {
        elevation.forward();
        color.next();
        shadowColor.value = Colors.grey;
      },
      child: AnimatedPhysicalModel(
        elevation: elevation.value,
        color: color.value,
        shadowColor: shadowColor.value,
        shape: BoxShape.circle,
        child: Container(
          width: 100.0,
          height: 100.0,
        ),
      ),
    );
  }
}
```
5. Finally, use the `AnimatedPhysicalModel` widget along with the animated values from the hook in your UI. The `GestureDetector` enables you to trigger the animations when a tap event occurs.

That's it! You now have an animated physical model in your Flutter application using Flutter Hooks. It's a great way to add subtle animations and interactivity to your UIs.

## Conclusion

The `useAnimatedPhysicalModel` hook in Flutter Hooks provides a simple and elegant way to create animated physical models in your Flutter applications. By leveraging the power of hooks, you can easily manage the animation parameters and control various aspects of your physical model's visual appearance.

So, give it a try and explore the possibilities of creating visually appealing and interactive UIs in Flutter using the `useAnimatedPhysicalModel` hook!

#FlutterHooks #AnimatedPhysicalModel