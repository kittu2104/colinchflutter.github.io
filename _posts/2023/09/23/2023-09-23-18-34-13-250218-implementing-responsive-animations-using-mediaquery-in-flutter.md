---
layout: post
title: "Implementing responsive animations using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [flutter, responsive, animations]
comments: true
share: true
---

In this post, we will explore how to create responsive animations in Flutter using the `MediaQuery` class. Flutter provides a powerful way to build beautiful and flexible user interfaces, and by combining it with MediaQuery, we can create animations that adapt to different screen sizes.

## What is MediaQuery?

`MediaQuery` is a class in the Flutter framework that provides information about the device's screen and its configuration. It allows us to retrieve information such as the screen size, orientation, device pixel density, and more.

## Creating Animation Widgets

To create a responsive animation, we need to define an animation widget that updates based on the screen size. First, let's import the necessary libraries:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/rendering.dart';
```

Next, we'll define our animation widget. For simplicity, let's create a widget that animates the opacity of a container:

```dart
class ResponsiveOpacityAnimation extends StatefulWidget {
  @override
  _ResponsiveOpacityAnimationState createState() =>
      _ResponsiveOpacityAnimationState();
}

class _ResponsiveOpacityAnimationState extends State<ResponsiveOpacityAnimation>
    with SingleTickerProviderStateMixin {
  AnimationController _animationController;
  Animation<double> _opacityAnimation;

  @override
  void initState() {
    super.initState();
    _animationController = AnimationController(
        vsync: this, duration: Duration(milliseconds: 500));
    _opacityAnimation = Tween<double>(begin: 0.0, end: 1.0).animate(
        CurvedAnimation(parent: _animationController, curve: Curves.easeInOut));
    _animationController.forward();
  }

  @override
  void dispose() {
    _animationController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return AnimatedBuilder(
      animation: _animationController,
      builder: (context, child) {
        return Opacity(
          opacity: _opacityAnimation.value,
          child: Container(
            width: MediaQuery.of(context).size.width * 0.8,
            height: MediaQuery.of(context).size.height * 0.3,
            color: Colors.blue,
          ),
        );
      },
    );
  }
}
```

In the above code, we define a `ResponsiveOpacityAnimation` widget that extends `StatefulWidget`. Inside, we use an `AnimationController` and `Animation` class to define an opacity animation that goes from 0.0 to 1.0 over a duration of 500 milliseconds. We then use the `AnimatedBuilder` widget to rebuild the `Opacity` widget whenever the animation value changes.

Notice how we use `MediaQuery.of(context)` to retrieve the screen size and adjust the width and height of the container accordingly. This ensures that the animation adapts to the available screen space.

## Using the Animation Widget

To use the `ResponsiveOpacityAnimation` widget in our app, we simply need to add it as a child widget to any other widget, such as a `Column` or `Row`. Let's see an example:

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Responsive Animations'),
        ),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Text(
                'Welcome!',
                style: TextStyle(
                  fontSize: 24.0,
                  fontWeight: FontWeight.bold,
                ),
              ),
              SizedBox(height: 20),
              ResponsiveOpacityAnimation(),
            ],
          ),
        ),
      ),
    );
  }
}

void main() {
  runApp(MyApp());
}
```

In the example above, we use the `ResponsiveOpacityAnimation` widget as a child of a `Column` widget. The animation will adapt to the available screen space and animate its opacity accordingly.

## Conclusion

By using the `MediaQuery` class in Flutter, we can create responsive animations that adapt to different screen sizes. In this post, we explored how to define an animation widget that adjusts its size based on the screen size and animates accordingly. With this knowledge, you can now create stunning and adaptive animations in your Flutter apps.

#flutter #responsive #animations