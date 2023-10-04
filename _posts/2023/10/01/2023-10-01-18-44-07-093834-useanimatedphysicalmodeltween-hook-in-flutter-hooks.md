---
layout: post
title: "useAnimatedPhysicalModelTween hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: [FlutterHooks]
comments: true
share: true
---

Flutter Hooks is a powerful package that enhances the functionality of Flutter by providing a set of hooks to simplify state management and widget composition. One of the interesting hooks offered by Flutter Hooks is `useAnimatedPhysicalModelTween`, which allows for smooth transitions between different physical models in your Flutter applications.

## What is a Physical Model?

In Flutter, a physical model represents a shape with material properties such as color, shadow, elevation, and more. Physical models are an essential part of creating visually appealing and interactive interfaces.

## The `useAnimatedPhysicalModelTween` Hook

The `useAnimatedPhysicalModelTween` hook in Flutter Hooks enables you to create smooth transitions between different physical models. By using this hook, you can dynamically change the properties of physical models over time, resulting in visually stunning animations.

## Usage

To use the `useAnimatedPhysicalModelTween` hook, make sure you have the `flutter_hooks` package added to your `pubspec.yaml` file. Then, import the necessary dependencies in your Dart file:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_hooks/flutter_hooks.dart';
```

Next, define your widget function and use the `useAnimatedPhysicalModelTween` hook within it:

```dart
Widget MyAnimatedContainer() {
  final borderRadius = useState(BorderRadius.circular(12.0));
  final elevation = useState(4.0);
  final color = useState(Colors.blue);

  final modelTween = useAnimatedPhysicalModelTween(
    borderRadius: borderRadius.value,
    elevation: elevation.value,
    color: color.value,
    child: Container(),
  );

  return GestureDetector(
    onTap: () {
      borderRadius.value = BorderRadius.circular(24.0);
      elevation.value = 8.0;
      color.value = Colors.red;
    },
    child: Scaffold(
      body: Center(
        child: AnimatedPhysicalModel(
          borderRadius: modelTween.borderRadius.value,
          elevation: modelTween.elevation.value,
          color: modelTween.color.value,
          child: Container(
            width: 200.0,
            height: 200.0,
          ),
        ),
      ),
    ),
  );
}
```

In the above example, we define three state variables (`borderRadius`, `elevation`, and `color`) using the `useState` hook from Flutter Hooks. These variables hold the values for the properties of our physical model.

We then use the `useAnimatedPhysicalModelTween` hook to create an animation tween based on the current values of the state variables. This tween is used within the `AnimatedPhysicalModel` widget to animate the changes in the physical model properties.

Finally, we wrap the `AnimatedPhysicalModel` widget with a `GestureDetector`, allowing the user to trigger the animation by tapping on the container. The animation changes the values of the `borderRadius`, `elevation`, and `color` state variables, resulting in a smooth transition.

## Conclusion

The `useAnimatedPhysicalModelTween` hook in Flutter Hooks simplifies the process of creating smooth transitions between physical models in your Flutter applications. By utilizing this hook, you can enhance the interactivity and visual appeal of your UI, resulting in a more engaging user experience.

#Flutter #FlutterHooks