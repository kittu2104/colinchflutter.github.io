---
layout: post
title: "Using the ScaleTransition widget with the Opacity widget for fade-in and scale animations"
description: " "
date: 2023-09-25
tags: [Animation]
comments: true
share: true
---

In Flutter, creating animations can bring life to your app and provide a better user experience. The `ScaleTransition` widget allows you to animate a widget's size and `Opacity` widget enables fading in and out of a widget. By combining these two widgets, you can achieve fade-in and scale animations simultaneously.

## Setting up the Animation

To start, import the required packages:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';
```

Next, create a `StatefulWidget` called `FadeScaleAnimation`:

```dart
class FadeScaleAnimation extends StatefulWidget {
  @override
  _FadeScaleAnimationState createState() => _FadeScaleAnimationState();
}
```

In the `_FadeScaleAnimationState` class, we define the necessary variables for the animations:

```dart
class _FadeScaleAnimationState extends State<FadeScaleAnimation>
    with SingleTickerProviderStateMixin {
  AnimationController _controller;
  Animation<double> _animationScale;
  Animation<double> _animationFade;

  @override
  void initState() {
    super.initState();

    // Initialize the animation controller
    _controller = AnimationController(
      duration: const Duration(milliseconds: 500),
      vsync: this,
    );

    // Define the scale animation
    _animationScale = Tween<double>(begin: 0, end: 1).animate(
      CurvedAnimation(
        parent: _controller,
        curve: Curves.ease,
      ),
    );

    // Define the fade animation
    _animationFade = Tween<double>(begin: 0, end: 1).animate(
      CurvedAnimation(
        parent: _controller,
        curve: Curves.ease,
      ),
    );

    // Start the animation
    _controller.forward();
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return AnimatedBuilder(
      animation: _controller,
      builder: (context, child) {
        return Transform.scale(
          scale: _animationScale.value,
          child: Opacity(
            opacity: _animationFade.value,
            child: child,
          ),
        );
      },
      child: // Your widget to be animated,
    );
  }
}
```

## Implementing the Animation

To use the fade-in and scale animation in your app, simply wrap the desired widget with the `FadeScaleAnimation` widget:

```dart
FadeScaleAnimation(
  child: // Your widget to be animated,
),
```

Remember to replace `// Your widget to be animated` with your own desired widget, such as `Container`, `Image`, or any other `Widget` you want to apply the animation to.

## Conclusion

By combining the `ScaleTransition` widget with the `Opacity` widget, you can easily create fade-in and scale animations in Flutter. Feel free to experiment with different animation durations and curves to achieve the desired effect.

#Flutter #Animation