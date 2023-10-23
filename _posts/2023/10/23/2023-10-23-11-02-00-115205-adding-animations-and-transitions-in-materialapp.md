---
layout: post
title: "Adding animations and transitions in MaterialApp."
description: " "
date: 2023-10-23
tags: [animations]
comments: true
share: true
---

Animations and transitions can greatly enhance the user experience in your Flutter applications. In this blog post, we will explore how to add animations and transitions in a MaterialApp widget.

## Table of Contents
- [Introduction](#introduction)
- [Getting Started](#getting-started)
- [Adding Animations](#adding-animations)
- [Adding Transitions](#adding-transitions)
- [Conclusion](#conclusion)

## Introduction
Animations and transitions bring life to your application by adding movement and smooth transitions between different screens or elements. They not only make your app look visually appealing but also provide important visual cues to the user.

## Getting Started
To get started, make sure you have Flutter installed and set up on your machine. Create a new Flutter project and open the main.dart file.

## Adding Animations
1. Import the `animation` library from Flutter:
```dart
import 'package:flutter/animation.dart';
```

2. Create an animation controller:
```dart
AnimationController _controller;
```
   
3. Initialize the animation controller in the `initState()` method:
```dart
@override
void initState() {
  super.initState();
  _controller = AnimationController(
    duration: const Duration(milliseconds: 500),
    vsync: this,
  );
}
```

4. Add animation to a widget:
```dart
AnimatedContainer(
  duration: Duration(milliseconds: 500),
  height: _controller.value * 100, // Use the value to animate the property
  child: // your widget here,
),
```

5. Start the animation:
```dart
_controller.forward();
```

Adding animations to your widgets will make them transition smoothly and create a more engaging user experience.

## Adding Transitions
Transitions are used to animate the screen navigation between different routes in your application. Here's how you can add transitions to a `MaterialApp` widget:

1. Import the `material` library from Flutter:
```dart
import 'package:flutter/material.dart';
```

2. Wrap your `MaterialApp` widget with a `PageRouteBuilder` and set the `pageBuilder` property to define the route transition:
```dart
MaterialApp(
  home: PageRouteBuilder(
    pageBuilder: (_, __, ___) => HomeScreen(),
    transitionsBuilder: (_, animation, __, child) {
      return FadeTransition(
        opacity: animation,
        child: child,
      );
    },
  ),
),
```

3. Define the transition animation. In this example, we are using a `FadeTransition`, which fades in the new screen:
```dart
transitionsBuilder: (_, animation, __, child) {
  return FadeTransition(
    opacity: animation,
    child: child,
  );
},
```

With transitions added to your application, moving between screens becomes visually more appealing and intuitive for the user.

## Conclusion
In this blog post, we explored how to add animations and transitions in a MaterialApp widget in Flutter. By adding animations to your widgets and transitions to your app's navigation, you can greatly enhance the user experience of your application.#

Have you tried adding animations and transitions in your Flutter apps? Let us know your experience in the comments below!

\#flutter #animations