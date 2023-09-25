---
layout: post
title: "Using the AnimatedPositioned widget with the Opacity widget for fade-in and position animations"
description: " "
date: 2023-09-25
tags: [flutter, animations]
comments: true
share: true
---

In Flutter, we can achieve fade-in and position animations using the `AnimatedPositioned` widget in combination with the `Opacity` widget. This powerful combination allows us to smoothly animate the opacity and position of a widget, creating visually appealing effects.

## AnimatedPositioned Widget

The `AnimatedPositioned` widget is built on top of the `Positioned` widget and allows us to animate the position of a widget within a `Stack`. It has specific properties such as `top`, `bottom`, `left`, and `right` which control the position of the widget within the stack.

To animate the position, we can wrap the `AnimatedPositioned` widget inside an `AnimatedContainer` and change the values of the position properties over time. This will result in a smooth animation of the widget's position.

## Opacity Widget

The `Opacity` widget is used to control the opacity of a widget. By changing the value of the `opacity` property, we can gradually fade a widget in or out. Setting the `opacity` to 0.0 will make the widget completely transparent, while setting it to 1.0 will make the widget fully visible.

## Combining AnimatedPositioned and Opacity

To create a fade-in and position animation, we can nest the `AnimatedPositioned` widget inside an `Opacity` widget. By animating the `top`, `left`, or any other position property of the `AnimatedPositioned` and changing the `opacity` value, we can achieve both position and fade-in animations simultaneously.

```dart
AnimatedOpacity(
  opacity: _fadeIn ? 1.0 : 0.0,
  duration: Duration(milliseconds: 500),
  child: AnimatedPositioned(
    top: _positioned ? 100 : 0,
    left: _positioned ? 100 : 0,
    duration: Duration(milliseconds: 500),
    child: Container(
      width: 200,
      height: 200,
      color: Colors.blue,
    ),
  ),
)
```

In the example code above, we have an `AnimatedOpacity` widget that controls the fade-in animation. The `_fadeIn` variable determines whether the widget should be visible or not. When set to `true`, the opacity is 1.0, making the widget visible. When set to `false`, the opacity is 0.0, rendering the widget completely transparent.

Inside the `AnimatedOpacity` widget, we have an `AnimatedPositioned` widget. The `_positioned` variable determines whether the widget should be positioned or not. When set to `true`, the widget will be positioned at `top: 100` and `left: 100`. When set to `false`, the widget will be positioned at `top: 0` and `left: 0`.

By changing the values of `_fadeIn` and `_positioned` variables or using animations to toggle them, we can create dynamic and interactive fade-in and position animations.

#flutter #animations