---
layout: post
title: "useAnimatedContainerTween hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: [FlutterHooks, useAnimatedContainerTween]
comments: true
share: true
---

In Flutter, Hooks are a way to write reusable and stateful logic in a functional manner. They provide an alternative approach to using StatefulWidget and manage the lifecycle and state of a widget.

One of the useful hooks provided by the Flutter Hooks package is `useAnimatedContainerTween`. This hook allows you to animate the changes in a widget's properties using a `Tween`. It simplifies the process of creating animations and makes them more declarative.

To use the `useAnimatedContainerTween` hook, follow these steps:

1. Install the Flutter Hooks package in your Flutter project:

```dart
dependencies:
  flutter_hooks: ^0.18.0
```

2. Import the required packages and hooks in your Dart file:

```dart
import 'package:flutter_hooks/flutter_hooks.dart';
import 'package:flutter/material.dart';
```

3. Define your widget and use the `useAnimatedContainerTween` hook:

```dart
class MyAnimatedWidget extends HookWidget {
  @override
  Widget build(BuildContext context) {
    final controller = useAnimationController(duration: Duration(seconds: 1));
    final widthTween = useAnimatedContainerTween<double>(
      initialValue: 100.0,
      targetValue: 300.0,
      curve: Curves.easeInOut,
      duration: Duration(seconds: 1),
    ).chain(CurveTween(curve: Curves.easeInOut));

    return AnimatedBuilder(
      animation: controller,
      builder: (context, child) {
        return Container(
          width: widthTween.evaluate(controller),
          height: 100.0,
          color: Colors.blue,
        );
      },
    );
  }
}
```

In the above code, we define a `MyAnimatedWidget` which uses the `useAnimatedContainerTween` hook to create an animation that changes the width of a `Container` widget from 100.0 to 300.0 over a duration of 1 second. We also specify the easing curve for the animation.

The `widthTween` returned by the `useAnimatedContainerTween` hook is then used inside an `AnimatedBuilder` widget to animate the `Container` width based on the value from the `widthTween` animation.

4. Use the widget in your app:

```dart
void main() {
  runApp(MaterialApp(
    home: Scaffold(
      appBar: AppBar(
        title: Text('My Animated Widget'),
      ),
      body: MyAnimatedWidget(),
    ),
  ));
}
```

That's it! Now you can use the `useAnimatedContainerTween` hook to easily create animations in your Flutter Hooks powered app.

## Conclusion

The `useAnimatedContainerTween` hook in Flutter Hooks provides a convenient way to create animations using the `Tween` concept. It simplifies the process of animating widget properties and makes animations more declarative. By using this hook, you can easily create smooth and visually appealing animations in your Flutter apps.

#FlutterHooks #useAnimatedContainerTween