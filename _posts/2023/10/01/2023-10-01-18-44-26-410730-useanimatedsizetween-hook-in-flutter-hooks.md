---
layout: post
title: "useAnimatedSizeTween hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: [FlutterHooks, AnimatedSizeTween]
comments: true
share: true
---

In Flutter Hooks, a fantastic package that enhances the capabilities of Flutter's widget framework, there is a hook called `useAnimatedSizeTween`. This hook is incredibly useful when you need to animate the size of a widget in your Flutter application.

## What is useAnimatedSizeTween?

`useAnimatedSizeTween` is a hook that allows you to create a smooth and seamless animation by automatically updating the widget's size based on a provided `sizeTween`. It leverages Flutter's animation system to animate the size transitions over a specific duration.

## How to use useAnimatedSizeTween?

To begin, make sure you have the Flutter Hooks package included in your project's dependencies.

1. Add the package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_hooks: ^0.18.0
```

2. Import the required hooks in your Dart file:

```dart
import 'package:flutter_hooks/flutter_hooks.dart';
```

3. Invoke the `useAnimatedSizeTween` hook with the desired `sizeTween` and `duration`.

```dart
Widget build(BuildContext context) {
  final sizeTween = SizeTween(begin: Size(100, 100), end: Size(200, 200));
  final animationDuration = const Duration(seconds: 1);

  return Scaffold(
    body: Center(
      child: useAnimatedSizeTween(
        sizeTween: sizeTween,
        duration: animationDuration,
        child: const MyWidget(),
      ),
    ),
  );
}
```

In the above code snippet, we are creating a `sizeTween` that defines the initial and final sizes of the widget. We also specify the `duration` of the animation.

4. The `useAnimatedSizeTween` hook returns a widget that dynamically adjusts the size of the child widget based on the provided `sizeTween` and `duration`. It is vital to ensure that the `useAnimatedSizeTween` is directly placed under a `Center` widget or any other widget that has a specific size constraint to prevent infinite growth or shrinkage.

## Conclusion

With the `useAnimatedSizeTween` hook from Flutter Hooks, animating the size of widgets in your Flutter application becomes a breeze. By providing the desired `sizeTween` and `duration`, you can easily enhance the visual appeal and user experience within your app.

Give it a try in your next Flutter project and unleash the power of seamless animations! #FlutterHooks #AnimatedSizeTween