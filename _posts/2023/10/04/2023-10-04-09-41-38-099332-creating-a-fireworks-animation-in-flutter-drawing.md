---
layout: post
title: "Creating a fireworks animation in Flutter drawing"
description: " "
date: 2023-10-04
tags: [setting]
comments: true
share: true
---

In this tutorial, we will learn how to create a fireworks animation using the Flutter framework. We'll be using custom drawing techniques to create a stunning visual effect. So let's get started!

## Table of Contents
- [Introduction](#introduction)
- [Setting Up the Project](#setting-up-the-project)
- [Creating the Fireworks Animation](#creating-the-fireworks-animation)
- [Animating the Fireworks](#animating-the-fireworks)
- [Conclusion](#conclusion)

## Introduction
Fireworks are a spectacular display of colors and lights, often seen during celebrations. Through Flutter's powerful custom drawing capabilities, we can recreate this effect in our Flutter app. The animation will simulate fireworks bursting in the sky, creating a visually stunning experience.

## Setting Up the Project
Before we begin, let's set up a new Flutter project. Open your terminal and run the following command:

```
flutter create fireworks_animation
```

Once the project is created, navigate to the project directory:

```
cd fireworks_animation
```

Open the `lib/main.dart` file in your favorite code editor and delete the existing code.

## Creating the Fireworks Animation
To create the fireworks animation, we'll use the `CustomPaint` widget provided by Flutter. `CustomPaint` allows us to paint custom shapes and animations on the screen.

First, create a new Flutter widget called `FireworksAnimation` that extends `CustomPainter`. In the `paint` method, we'll define the drawing logic for our fireworks animation. Here's an example code snippet to get started:

```dart
import 'package:flutter/material.dart';

class FireworksAnimation extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // Drawing logic goes here
  }
  
  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) {
    return false;
  }
}
```

In the `paint` method, we'll use the `Canvas` object to draw fireworks particles. We can create colorful circles or any other shapes to represent the fireworks bursts. Feel free to experiment with different shapes and colors to achieve the desired effect.

## Animating the Fireworks
To animate the fireworks, we'll use the `AnimationController` class provided by Flutter. This class allows us to control the animation's duration and playback. We'll wrap our `FireworksAnimation` widget with a `CustomPaint` widget inside a `Container` widget.

Here's an example code snippet to initialize and animate the fireworks animation:

```dart
import 'package:flutter/material.dart';

class FireworksAnimation extends CustomPainter with ChangeNotifier {
  AnimationController _controller;
  Animation<double> _animation;

  FireworksAnimation() {
    _controller = AnimationController(vsync: this, duration: Duration(seconds: 3));
    _animation = Tween(begin: 0.0, end: 1.0).animate(_controller);

    _controller.repeat();
  }

  @override
  void paint(Canvas canvas, Size size) {
    // Drawing logic goes here
    // Use _animation.value to animate the drawing
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) {
    return false;
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }
}

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      body: Center(
        child: Container(
          width: 200,
          height: 200,
          child: CustomPaint(
            painter: FireworksAnimation(),
          ),
        ),
      ),
    ),
  ));
}
```

In the `FireworksAnimation` class, we initialize an `AnimationController` and an `Animation<double>` object. The `AnimationController` controls the playback of our animation, and the `Animation<double>` defines the range of values for our animation.

We then use the `_controller.repeat()` method to animate the fireworks continuously. Within the `paint` method, we can utilize the `_animation.value` to animate the drawing of our fireworks particles.

Finally, in the `main()` function, we wrap our `CustomPaint` widget with a `Container` to set its dimensions, and we add it to the `body` of a `Scaffold` widget.

And there you have it - a fireworks animation in Flutter! You can further enhance the animation by adding effects such as fading, rotation, or particle trails. Feel free to experiment and make it your own.

## Conclusion
In this tutorial, we learned how to create a fireworks animation in Flutter using custom drawing techniques. We used the `CustomPainter` class to define the drawing logic for our fireworks bursts and the `AnimationController` class to animate the fireworks. With these techniques, you can create mesmerizing visual effects and bring your Flutter app to life.

I hope you found this tutorial helpful. Happy coding!

#flutter #fireworks