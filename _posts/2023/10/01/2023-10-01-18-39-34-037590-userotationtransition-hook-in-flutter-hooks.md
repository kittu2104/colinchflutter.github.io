---
layout: post
title: "useRotationTransition hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: [Flutter, FlutterHooks]
comments: true
share: true
---

In Flutter, animations play a vital role in creating engaging and interactive user interfaces. Flutter Hooks is a package that provides a set of reusable hooks that simplify the process of managing state and performing animations in Flutter apps. One such hook is `useRotationTransition`, which allows us to easily animate the rotation of a widget in response to changes in state.

## Installation

Before we can use the `useRotationTransition` hook, we need to add the Flutter Hooks package to our project. Open your `pubspec.yaml` file and add the following line to the `dependencies` section:

```dart
dependencies:
  flutter_hooks: ^0.18.0
```

After adding the dependency, run `flutter pub get` to fetch the package.

## Usage

To use the `useRotationTransition` hook, we first need to import it:

```dart
import 'package:flutter_hooks/flutter_hooks.dart';
```

Next, let's create a StatefulWidget where we will be using the hook. Inside the `build` method of the widget, we can use the `useRotationTransition` hook to animate the rotation of a widget based on a given animation controller.

```dart
class MyWidget extends HookWidget {
  @override
  Widget build(BuildContext context) {
    final animationController = useAnimationController(duration: Duration(seconds: 2));
    final rotationAnimation = useRotationTransition(animationController: animationController);

    return RotationTransition(
      turns: rotationAnimation,
      child: Container(
        width: 200,
        height: 200,
        color: Colors.blue,
        child: Center(
          child: Text(
            'Hello Hooks',
            style: TextStyle(
              fontSize: 24,
              color: Colors.white,
            ),
          ),
        ),
      ),
    );
  }
}
```

In the above code, we first create an `AnimationController` using the `useAnimationController` hook and specify the duration of the animation. We then pass this animation controller to the `useRotationTransition` hook, which returns an animation that we can use in the `turns` property of the `RotationTransition` widget.

Finally, we wrap our content in the `RotationTransition` widget, which will animate the rotation of the child widget based on the provided animation.

## Conclusion

The `useRotationTransition` hook in Flutter Hooks simplifies the process of animating the rotation of a widget. By using this hook, we can create dynamic and engaging animations in our Flutter apps with ease.

Make sure to include the `flutter_hooks` dependency in your `pubspec.yaml` file and import the necessary packages to use the hook in your project. With a little bit of code, you can bring your app to life with smooth and visually appealing rotating animations!

**#Flutter #FlutterHooks**