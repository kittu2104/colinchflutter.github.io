---
layout: post
title: "usePositionedTransitionTween hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: [flutter, flutterhooks]
comments: true
share: true
---

In Flutter, the `usePositionedTransitionTween` hook is a helpful utility provided by the Flutter Hooks library that allows you to create animated transitions for your widgets. This hook simplifies the process of animating the position and layout of a widget by using a `PositionedTransition` widget and a `Tween` animation.

## Installation

To use `usePositionedTransitionTween` hook, you need to first install the Flutter Hooks library into your Flutter project. Open your project's `pubspec.yaml` file and add the following dependency:

```yaml
dependencies:
  flutter_hooks: ^0.14.0
```

Save the changes and run `flutter pub get` to download the package.

## Usage

Once you have the Flutter Hooks library installed, you can start using the `usePositionedTransitionTween` hook in your Flutter project. Here's an example of how to use it:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_hooks/flutter_hooks.dart';

class MyAnimatedWidget extends HookWidget {
  @override
  Widget build(BuildContext context) {
    final position = usePositionedTransitionTween(
      duration: const Duration(seconds: 1),
      from: Offset(-100, 0),
      to: Offset(0, 0),
    );

    return Scaffold(
      appBar: AppBar(
        title: Text('PositionedTransition Example'),
      ),
      body: Center(
        child: AnimatedBuilder(
          animation: position,
          builder: (context, child) {
            return Container(
              width: 100,
              height: 100,
              color: Colors.blue,
              child: PositionedTransition(
                rect: position,
                child: Container(
                  color: Colors.red,
                ),
              ),
            );
          },
        ),
      ),
    );
  }
}

void main() {
  runApp(MaterialApp(
    home: MyAnimatedWidget(),
  ));
}
```

In this example, the `usePositionedTransitionTween` hook is used to create an animation that transitions a red container from an initial offset of (-100, 0) to a final offset of (0, 0). The `Duration` and initial and final positions are passed to the hook as parameters.

The `position` returned from `usePositionedTransitionTween` is then used as an animation value inside the `AnimatedBuilder`, which rebuilds the widget tree on every animation frame. The `PositionedTransition` widget is responsible for animating the position and layout of the red container, based on the `Animation` value provided.

By using the `usePositionedTransitionTween` hook, you can easily create smooth and animated transitions for your widgets in Flutter, making your app more engaging and interactive.

#flutter #flutterhooks