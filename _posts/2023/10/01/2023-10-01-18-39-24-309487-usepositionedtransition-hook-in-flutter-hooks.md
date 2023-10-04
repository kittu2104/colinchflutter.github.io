---
layout: post
title: "usePositionedTransition hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: [Hooks]
comments: true
share: true
---

In Flutter development, Hooks serve as a way to introduce stateful logic into a widget tree without the need for a StatefulWidget. Flutter Hooks provides a variety of built-in Hooks that can be used to enhance the functionality of your Flutter app. One such Hook is `usePositionedTransition`, which allows you to create animated transitions for positioning widgets.

## Installing Flutter Hooks

Before we dive into using the `usePositionedTransition` Hook, make sure that you have Flutter Hooks installed in your project. To do this, include the following dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_hooks: ^0.18.0
```

After adding the dependency, run `flutter pub get` to fetch the package.

## Using `usePositionedTransition`

The `usePositionedTransition` Hook enables you to create animated transitions for positioning widgets within a `Stack`. With this Hook, you can define the starting and ending positions for a widget, and Flutter will automatically animate the transition between the two positions.

Here's an example of how you can use the `usePositionedTransition` Hook:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_hooks/flutter_hooks.dart';

void main() => runApp(MyApp());

class MyApp extends HookWidget {
  @override
  Widget build(BuildContext context) {
    final animationController = useAnimationController(duration: Duration(seconds: 1));
    final positioning = usePositionedTransition(
      rect: Rect.fromLTRB(0, 0, 100, 100),
      animation: Tween<Rect>(
        begin: Rect.fromLTRB(0, 0, 100, 100),
        end: Rect.fromLTRB(100, 100, 200, 200),
      ).animate(animationController),
      child: Container(color: Colors.blue),
    );

    useEffect(() {
      animationController.repeat(reverse: true);
      return animationController.dispose;
    }, []);

    return MaterialApp(
      home: Scaffold(
        body: Stack(
          children: [
            positioning,
          ],
        ),
      ),
    );
  }
}
```

In this example, we first import the required packages: `flutter_hooks` and `flutter/material`. We then define a `MyApp` widget, which extends `HookWidget`. Inside the build method, we create an `animationController` using the `useAnimationController` Hook.

Next, we define the `positioning` variable using `usePositionedTransition`. We provide an initial rectangle for the widget's position and an animation that specifies the starting and ending positions using a `RectTween`. We also pass in the child widget that we want to animate. In this case, we use a simple `Container` with a blue color.

We use the `useEffect` Hook to start the animation by repeating the animationController and dispose it when the widget is unmounted.

Finally, we wrap the `positioning` widget inside a `Stack` to position it using the animated transition.

## Conclusion

The `usePositionedTransition` Hook in Flutter Hooks is a powerful tool for creating animated transitions for positioning widgets. By using this Hook, you can easily add smooth and visually appealing animations to your Flutter app. Give it a try and unleash its potential in your next Flutter project!

\[hashtags: #Flutter #Hooks\]