---
layout: post
title: "Using the PositionedTransition widget with the Opacity widget for animated opacity changes"
description: " "
date: 2023-09-25
tags: [animation]
comments: true
share: true
---

In Flutter, you can create eye-catching animations by combining different widgets together. The `PositionedTransition` widget and the `Opacity` widget can be used in tandem to achieve animated opacity changes in your Flutter app.

## What is the PositionedTransition widget?

The `PositionedTransition` widget helps you move and resize child widgets smoothly during animation. It takes a `rect` parameter and animates the child from one position to another within that rectangle.

## What is the Opacity widget?

The `Opacity` widget allows you to control the opacity of a child widget. By changing the opacity value, you can make the child widget appear gradually visible or invisible.

## How to use the PositionedTransition and Opacity widgets together?

To use the `PositionedTransition` widget with the `Opacity` widget for animated opacity changes, you can follow these steps:

1. Import the necessary packages:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';
```

2. Wrap your widget with the `PositionedTransition` widget, specifying the desired `rect` parameter and an animation controller:

```dart
PositionedTransition(
  rect: RectTween(
    begin: Rect.fromLTWH(0, 0, 100, 100),
    end: Rect.fromLTWH(100, 100, 200, 200),
  ).animate(animationController),
  child: Opacity(
    opacity: animationController.value,
    child: YourWidget(),
  ),
)
```

3. Create an animation controller and start the animation:

```dart
class MyWidgetState extends State<MyWidget> with SingleTickerProviderStateMixin {
  AnimationController animationController;

  @override
  void initState() {
    super.initState();
    animationController = AnimationController(
      duration: Duration(seconds: 1),
      vsync: this,
    )..repeat();
  }

  @override
  void dispose() {
    animationController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return PositionedTransition(
      rect: RectTween(
        begin: Rect.fromLTWH(0, 0, 100, 100),
        end: Rect.fromLTWH(100, 100, 200, 200),
      ).animate(animationController),
      child: Opacity(
        opacity: animationController.value,
        child: YourWidget(),
      ),
    );
  }
}
```

In this example, the `PositionedTransition` widget animates the position of the child widget from `(0, 0, 100, 100)` to `(100, 100, 200, 200)` based on the animation controller. At the same time, the `Opacity` widget changes the opacity of the child widget smoothly as the animation progresses.

## Conclusion

The combination of the `PositionedTransition` and `Opacity` widgets in Flutter allows you to create visually appealing animated opacity changes. By leveraging these widgets, you can enhance the user experience of your Flutter app and create compelling visual effects. #flutter #animation