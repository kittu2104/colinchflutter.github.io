---
layout: post
title: "Drawing animations in Flutter"
description: " "
date: 2023-10-04
tags: [animation]
comments: true
share: true
---

Flutter is a powerful framework that allows you to build beautiful and interactive user interfaces. One of the key features of Flutter is its ability to create smooth, fluid animations. In this blog post, we will explore how to draw animations in Flutter using the built-in animation API.

## Table of Contents
1. What are Flutter animations?
2. Getting started with animations in Flutter
3. Creating a basic animation
4. Adding interactivity to animations
5. Animating custom shapes
6. Conclusion

## 1. What are Flutter animations?

Animations in Flutter are a way to bring user interfaces to life by adding movement and transition effects. They enhance the overall user experience and make the app feel more engaging and responsive. Flutter provides an animation API that allows you to create various types of animations, such as fading, scaling, sliding, and rotating.

## 2. Getting started with animations in Flutter

To get started with animations in Flutter, you need to import the `animation` package and create an `AnimationController` object. The `AnimationController` is responsible for controlling the animation, including starting, stopping, and defining the duration and curve of the animation.

```dart
import 'package:flutter/material.dart';

class MyAnimationWidget extends StatefulWidget {
  @override
  _MyAnimationWidgetState createState() => _MyAnimationWidgetState();
}

class _MyAnimationWidgetState extends State<MyAnimationWidget>
    with SingleTickerProviderStateMixin {
  AnimationController _controller;
  Animation<double> _animation;

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: Duration(seconds: 2),
      vsync: this,
    );
    _animation = Tween<double>(begin: 0, end: 200).animate(_controller);
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
      animation: _animation,
      builder: (BuildContext context, Widget child) {
        return Container(
          width: _animation.value,
          height: _animation.value,
          color: Colors.blue,
        );
      },
    );
  }
}
```

## 3. Creating a basic animation

In the code snippet above, we create a basic animation that increases the size of a container from 0 to 200 pixels over a duration of 2 seconds. We use the `AnimatedBuilder` widget to rebuild the UI whenever the animation value changes.

To start the animation, we call `_controller.forward()`. To stop the animation, we call `_controller.stop()`. You can also reverse the animation by calling `_controller.reverse()`.

## 4. Adding interactivity to animations

Flutter also allows you to add interactivity to your animations. For example, you can create animations that respond to user gestures, such as swiping or tapping. To achieve this, you can use gesture detectors and combine them with animations.

```dart
import 'package:flutter/material.dart';

class InteractiveAnimation extends StatefulWidget {
  @override
  _InteractiveAnimationState createState() => _InteractiveAnimationState();
}

class _InteractiveAnimationState extends State<InteractiveAnimation> {
  AnimationController _controller;
  Animation<double> _animation;

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: Duration(seconds: 1),
      vsync: this,
    );
    _animation = Tween<double>(begin: 100, end: 200).animate(_controller);
  }

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTap: () {
        if (_controller.isCompleted) {
          _controller.reverse();
        } else {
          _controller.forward();
        }
      },
      child: AnimatedBuilder(
        animation: _animation,
        builder: (BuildContext context, Widget child) {
          return Container(
            width: _animation.value,
            height: _animation.value,
            color: Colors.blue,
          );
        },
      ),
    );
  }
}
```

In the code snippet above, we create an animation that increases the size of a container when it is tapped and decreases the size when tapped again. We achieve this by toggling the animation between forward and reverse states using the `onTap` callback of the `GestureDetector` widget.

## 5. Animating custom shapes

Apart from animating basic widgets like containers, Flutter also allows you to animate custom shapes. You can use the `CustomPainter` class to define your own shapes and animations.

```dart
import 'package:flutter/material.dart';

class CustomShapeAnimation extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return AnimatedBuilder(
      animation: _animation,
      builder: (BuildContext context, Widget child) {
        return CustomPaint(
          painter: MyPainter(_animation.value),
        );
      },
    );
  }
}

class MyPainter extends CustomPainter {
  final double value;

  MyPainter(this.value);

  @override
  void paint(Canvas canvas, Size size) {
    // Draw custom shape based on the animation value
  }

  @override
  bool shouldRepaint(MyPainter oldDelegate) {
    return value != oldDelegate.value;
  }
}
```

In the code snippet above, we use the `CustomPaint` widget and implement a custom `MyPainter` class that extends `CustomPainter`. In the `MyPainter` class, we define the shape and size of the custom shape based on the animation value.

## 6. Conclusion

In this blog post, we explored how to draw animations in Flutter using the built-in animation API. We learned how to create basic animations, add interactivity, and animate custom shapes. Flutter's animation capabilities provide endless possibilities for creating engaging and visually appealing user interfaces.

Remember to experiment and play around with different animations and effects to make your Flutter app truly stand out!

#flutter #animation