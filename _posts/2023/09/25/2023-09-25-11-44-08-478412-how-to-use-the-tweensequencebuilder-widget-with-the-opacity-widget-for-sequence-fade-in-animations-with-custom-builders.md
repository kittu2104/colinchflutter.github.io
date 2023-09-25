---
layout: post
title: "How to use the TweenSequenceBuilder widget with the Opacity widget for sequence fade-in animations with custom builders"
description: " "
date: 2023-09-25
tags: [flutter, animation]
comments: true
share: true
---

In Flutter, animations can be created using various animation classes and widgets. One common scenario is to create a sequence of animations, where one animation starts after another animation has completed. 

In this tutorial, we will learn how to use the `TweenSequenceBuilder` widget with the `Opacity` widget to create sequence fade-in animations with custom builders.

## Step 1: Add Dependencies and Import Libraries

To use the `TweenSequenceBuilder` widget, we need to add the `flutter` dependency to the `pubspec.yaml` file and import the necessary libraries. Open the `pubspec.yaml` file and add the following dependency:

```yaml
dependencies:
  flutter:
    sdk: flutter
```

After adding the dependency, save the file and let Flutter download the required packages.

## Step 2: Create a StatefulWidget 

Create a new file, for example, `fade_in_animation.dart`, and define a new `StatefulWidget` class called `FadeInAnimation`.

```dart
import 'package:flutter/material.dart';

class FadeInAnimation extends StatefulWidget {
  @override
  _FadeInAnimationState createState() => _FadeInAnimationState();
}
```

## Step 3: Create a State Class

Inside the `fade_in_animation.dart` file, create a new `State` class called `_FadeInAnimationState` that extends the `State<FadeInAnimation>`.

```dart
class _FadeInAnimationState extends State<FadeInAnimation> {
  // TODO: Implement the state logic
}
```

## Step 4: Initialize Animation Controllers and Values

In the `_FadeInAnimationState` class, declare the necessary variables. We need an animation controller and a list of `TweenSequenceItem<double>` objects.

```dart
class _FadeInAnimationState extends State<FadeInAnimation> with TickerProviderStateMixin {
  AnimationController _controller;
  List<TweenSequenceItem<double>> _tweenSequenceItems;
  
  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      vsync: this,
      duration: const Duration(milliseconds: 1000),
    );
    
    _tweenSequenceItems = [
      TweenSequenceItem<double>(
        tween: Tween<double>(begin: 0.0, end: 1.0),
        weight: 1.0,
      ),
      TweenSequenceItem<double>(
        tween: Tween<double>(begin: 1.0, end: 0.0),
        weight: 1.0,
      ),
    ];
  }
  
  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }
  
  @override
  Widget build(BuildContext context) {
    return Container(
      // TODO: Implement the widget tree
    );
  }
}
```

In this code, we initialized an animation controller `_controller` and set the duration of the animation to 1000 milliseconds. We also created our list of `TweenSequenceItem<double>` objects `_tweenSequenceItems`. This list defines the sequence of fade-in and fade-out animations.

The `TweenSequenceItem` takes a `tween`, which specifies the range of values for the animation, and a `weight` that defines the duration of this particular animation sequence item.

## Step 5: Implement Fade In Animation Widget

Inside the `build` method of the `_FadeInAnimationState` class, implement the fade-in animation using the `TweenSequenceBuilder` and `Opacity` widgets.

```dart
@override
Widget build(BuildContext context) {
  return Container(
    child: Center(
      child: TweenSequenceBuilder<double>(
        tween: TweenSequence<double>(_tweenSequenceItems),
        builder: (BuildContext context, double value, _) {
          return Opacity(
            opacity: value,
            child: Text(
              'Fade-in Animation',
              style: TextStyle(
                fontSize: 24.0,
                fontWeight: FontWeight.bold,
              ),
            ),
          );
        },
      ),
    ),
  );
}
```

In this code, we used the `Center` widget to align the child content in the center of the container. Inside the `TweenSequenceBuilder` widget, we passed our list of `TweenSequenceItem<double>` objects `_tweenSequenceItems` to the `tween` property. 

Inside the `builder` function, we used the `Opacity` widget to fade the text in and out based on the value provided by the `TweenSequenceBuilder`. We set the `opacity` property of the `Opacity` widget to the current value and the child content to the text that we want to animate.

## Step 6: Start and Stop the Animation

To start and stop the animation, we need to call the appropriate methods of the animation controller. We can trigger these methods based on user interaction or any other events. For simplicity, we will start the animation when the widget is visible on the screen.

In the `_FadeInAnimationState` class, modify the `initState` method and the `build` method as shown below:

```dart
@override
void initState() {
  super.initState();
  _controller = AnimationController(
    vsync: this,
    duration: const Duration(milliseconds: 1000),
  );
  
  _tweenSequenceItems = [
    TweenSequenceItem<double>(
      tween: Tween<double>(begin: 0.0, end: 1.0),
      weight: 1.0,
    ),
    TweenSequenceItem<double>(
      tween: Tween<double>(begin: 1.0, end: 0.0),
      weight: 1.0,
    ),
  ];
  
  _controller.forward();
}

@override
Widget build(BuildContext context) {
  return Container(
    child: Center(
      child: AnimatedBuilder(
        animation: _controller,
        builder: (BuildContext context, Widget child) {
          return Opacity(
            opacity: _controller.value,
            child: Text(
              'Fade-in Animation',
              style: TextStyle(
                fontSize: 24.0,
                fontWeight: FontWeight.bold,
              ),
            ),
          );
        },
      ),
    ),
  );
}
```

In this code, we called the `_controller.forward()` method in the `initState` method to start the animation when the widget is first initialized. We also used the `AnimatedBuilder` widget instead of the `TweenSequenceBuilder` widget to rebuild the `Opacity` widget whenever the animation value changes.

## Step 7: Add the FadeInAnimation Widget

Finally, to use the `FadeInAnimation` widget in your app, simply add it to the desired screen or widget tree.

```dart
class MyScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Animation Example'),
      ),
      body: Center(
        child: FadeInAnimation(),
      ),
    );
  }
}
```

By following these steps, you can create fade-in animations using the `TweenSequenceBuilder` widget with the `Opacity` widget and customize the animations using custom builders. Feel free to experiment with different properties and values to achieve the desired animation effects.

#flutter #animation