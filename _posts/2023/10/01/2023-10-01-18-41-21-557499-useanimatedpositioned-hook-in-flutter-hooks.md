---
layout: post
title: "useAnimatedPositioned hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: [FlutterHooks]
comments: true
share: true
---

If you're familiar with Flutter development, you may have come across the `AnimatedPositioned` widget, which allows you to animate the position of a child widget within a stack. Flutter Hooks provides a convenient hook called `useAnimatedPositioned` that simplifies using `AnimatedPositioned` in a functional way.

## Installing Flutter Hooks

Before we dive into using the `useAnimatedPositioned` hook, make sure you have Flutter Hooks installed in your project. You can add it as a dependency in your `pubspec.yaml` file:

```dart
dependencies:
  flutter_hooks: ^0.18.0
```

### Importing Dependencies
To use the `useAnimatedPositioned` hook, add the following import statement to your Dart file:

```dart
import 'package:flutter_hooks/flutter_hooks.dart';
```

## Using the `useAnimatedPositioned` Hook

The `useAnimatedPositioned` hook works similarly to other Flutter Hooks, such as `useAnimationController`. It returns a mutable value, which represents the position of the child widget. You can use this value to animate the positioning of your widget.

Here's an example of how you can use the `useAnimatedPositioned` hook:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_hooks/flutter_hooks.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends HookWidget {
  @override
  Widget build(BuildContext context) {
    final position = useAnimatedPositioned(
      duration: const Duration(seconds: 1),
      top: useState(0.0),
      left: useState(0.0),
    );

    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Flutter Hooks - useAnimatedPositioned'),
        ),
        body: Stack(
          children: [
            AnimatedPositioned(
              duration: position.duration,
              top: position.top,
              left: position.left,
              child: Container(
                width: 100,
                height: 100,
                color: Colors.blue,
              ),
            ),
            Positioned(
              bottom: 0,
              right: 0,
              child: ElevatedButton(
                onPressed: () {
  position.top.value += 50;
  position.left.value += 50;
                },
                child: Text('Animate'),
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

In this example, we created a `position` variable using the `useAnimatedPositioned` hook. We passed the desired duration, top value, and left value as arguments. Inside the `AnimatedPositioned` widget, we provided the animated values and added a `Container` to visualize the animation.

Finally, we added a `Positioned` widget with an `ElevatedButton` at the bottom-right corner of the `Stack`. This button allows us to animate the position of the child `Container` when clicked.

## Conclusion

Using the `useAnimatedPositioned` hook in Flutter Hooks simplifies animating the position of a child widget with the `AnimatedPositioned` widget. With the example provided above, you can easily incorporate this hook into your Flutter projects and create captivating animated user interfaces. Happy coding!

#Flutter #FlutterHooks