---
layout: post
title: "useAnimatedAlign hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: []
comments: true
share: true
---

In Flutter, `Hooks` is a package that provides a way to use stateful logic and lifecycle management in your functional widgets. One useful hook is `useAnimatedAlign`, which allows you to animate the alignment of a widget.

## Installation

Before we dive into using `useAnimatedAlign`, make sure you have installed the `flutter_hooks` package in your project. You can do this by adding the following line to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_hooks: ^0.16.0
```

Then, run the following command to download the package:

```bash
flutter pub get
```

Once the package is installed, you're ready to use the `useAnimatedAlign` hook in your project.

## Basic Usage

To use `useAnimatedAlign`, you'll need to import the required packages:

```dart
import 'package:flutter_hooks/flutter_hooks.dart';
import 'package:flutter/material.dart';
```

Then, inside your functional widget, you can use the hook like this:

```dart
Widget MyWidget() {
  final alignment = useState<Alignment>(Alignment.center);

  useAnimatedAlign(
    duration: const Duration(seconds: 1),
    alignment: alignment.value,
    child: Container(
      width: 200,
      height: 200,
      color: Colors.blue,
    ),
  );

  return Scaffold(
    body: GestureDetector(
      onTap: () {
        alignment.value = alignment.value == Alignment.center
            ? Alignment.topLeft
            : Alignment.center;
      },
      child: Center(
        child: Text('Tap to animate'),
      ),
    ),
  );
}
```

In the above code, we first create a state variable `alignment` using the `useState` hook from `flutter_hooks`. The initial value of `alignment` is set to `Alignment.center`, which is the default alignment for a widget.

Next, we call `useAnimatedAlign` and pass in the following parameters:

- `duration`: The duration of the animation.
- `alignment`: The current alignment value.
- `child`: The widget that we want to animate.

In this example, we use a `Container` widget as the child, but you can replace it with any widget of your choice. The `alignment` value will animate the position of the child widget when it changes.

Finally, we use a `GestureDetector` to detect taps on the screen. When tapped, the alignment value is updated to either `Alignment.topLeft` or `Alignment.center`, toggling the position of the child widget.

## Conclusion

The `useAnimatedAlign` hook in the Flutter Hooks package provides an easy way to animate the alignment of a widget in your functional Flutter widgets. By using this hook, you can create dynamic and interactive UIs with smooth animations.