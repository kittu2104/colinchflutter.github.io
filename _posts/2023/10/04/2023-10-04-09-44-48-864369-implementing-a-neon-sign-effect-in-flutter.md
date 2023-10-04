---
layout: post
title: "Implementing a neon sign effect in Flutter"
description: " "
date: 2023-10-04
tags: [prerequisites), setting]
comments: true
share: true
---

Flutter is a powerful framework for building beautiful user interfaces. With its customizable widgets and flexibility, it offers endless possibilities for creating stunning UI effects. One popular effect is the neon sign effect, which gives a vibrant and glowing appearance to text or other elements. In this tutorial, we will explore how to implement a neon sign effect in Flutter.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Setting up the Project](#setting-up-the-project)
- [Creating the Neon Sign Widget](#creating-the-neon-sign-widget)
- [Adding Animation](#adding-animation)
- [Conclusion](#conclusion)

## Prerequisites

To follow along with this tutorial, you will need a basic understanding of Flutter and have it set up on your machine. If you haven't installed Flutter yet, you can refer to the [official Flutter installation guide](https://flutter.dev/docs/get-started/install) for instructions.

## Setting up the Project

1. Open your preferred IDE and create a new Flutter project.
2. Replace the contents of the `lib/main.dart` file with the following code:

```dart
import 'package:flutter/material.dart';

void main() => runApp(NeonSignApp());

class NeonSignApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Neon Sign Effect',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: NeonSignPage(),
    );
  }
}

class NeonSignPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Neon Sign Effect'),
      ),
      body: Center(
        child: NeonSignWidget(text: 'Welcome to Flutter'),
      ),
    );
  }
}

class NeonSignWidget extends StatelessWidget {
  final String text;

  const NeonSignWidget({required this.text});

  @override
  Widget build(BuildContext context) {
    return Text(
      text,
      style: TextStyle(
        fontSize: 48,
        fontWeight: FontWeight.bold,
        color: Colors.white,
      ),
    );
  }
}

```

## Creating the Neon Sign Widget

In the code above, we defined a `NeonSignWidget` class that takes a `text` parameter and displays it using a white font color. To give it a neon effect, we will utilize the `Glow` widget from Flutter.

1. Update the `NeonSignWidget` class as follows:

```dart
class NeonSignWidget extends StatelessWidget {
  final String text;

  const NeonSignWidget({required this.text});

  @override
  Widget build(BuildContext context) {
    return Stack(
      children: [
        Text(
          text,
          style: TextStyle(
            fontSize: 48,
            fontWeight: FontWeight.bold,
            color: Colors.white,
          ),
        ),
        Positioned.fill(
          child: ClipRect(
            child: BackdropFilter(
              filter: ImageFilter.blur(sigmaX: 5, sigmaY: 5),
              child: Container(
                color: Colors.transparent,
              ),
            ),
          ),
        ),
        Text(
          text,
          style: TextStyle(
            fontSize: 48,
            fontWeight: FontWeight.bold,
            foreground: Paint()
              ..style = PaintingStyle.stroke
              ..strokeWidth = 4
              ..color = Colors.blue,
          ),
        ),
      ],
    );
  }
}
```

In the updated `NeonSignWidget` class, we use a `Stack` widget to layer multiple `Text` widgets on top of each other. The first `Text` widget displays the text as it is, with a white font color. The second `Text` widget overlays the first one with a neon glow effect by setting its `foreground` to a `Paint` object with a blue color and a stroke width of 4.

## Adding Animation

To make the neon sign effect more appealing, we can add animation to make the glow appear as if it is pulsating. Flutter provides various animation options, and we will utilize the `AnimationController` and `Tween` classes for this purpose.

1. Update the `NeonSignWidget` class as follows:

```dart
class NeonSignWidget extends StatefulWidget {
  final String text;

  const NeonSignWidget({required this.text});

  @override
  _NeonSignWidgetState createState() => _NeonSignWidgetState();
}

class _NeonSignWidgetState extends State<NeonSignWidget>
    with SingleTickerProviderStateMixin {
  late AnimationController _animationController;
  late Animation<double> _animation;

  @override
  void initState() {
    super.initState();
    _animationController = AnimationController(
      duration: const Duration(milliseconds: 750),
      vsync: this,
    )..repeat(reverse: true);
    _animation = Tween<double>(begin: 0.4, end: 1.0).animate(
      CurvedAnimation(
        parent: _animationController,
        curve: Curves.easeInOut,
      ),
    );
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
      builder: (BuildContext context, Widget? child) {
        return Opacity(
          opacity: _animation.value,
          child: Stack(
            children: [
              Text(
                widget.text,
                style: TextStyle(
                  fontSize: 48,
                  fontWeight: FontWeight.bold,
                  color: Colors.white,
                ),
              ),
              Positioned.fill(
                child: ClipRect(
                  child: BackdropFilter(
                    filter: ImageFilter.blur(sigmaX: 5, sigmaY: 5),
                    child: Container(
                      color: Colors.transparent,
                    ),
                  ),
                ),
              ),
              Text(
                widget.text,
                style: TextStyle(
                  fontSize: 48,
                  fontWeight: FontWeight.bold,
                  foreground: Paint()
                    ..style = PaintingStyle.stroke
                    ..strokeWidth = 4
                    ..color = Colors.blue,
                ),
              ),
            ],
          ),
        );
      },
    );
  }
}
```

In the updated code above, we made the `NeonSignWidget` a `StatefulWidget` and added an `_animationController` and an `_animation` variable. In the `initState` method, we set up the animation controller to run indefinitely with a duration of 750 milliseconds and a reversal between each iteration. We also define a tween animation that transitions the opacity of the glow effect from 0.4 to 1.0 using an ease-in-out curve.

Finally, we use the `AnimatedBuilder` widget to rebuild the widget whenever the animation value changes. We wrap the widget tree in an `Opacity` widget and set its alpha value to `_animation.value`, resulting in an animated pulsating glow effect.

## Conclusion

In this tutorial, we learned how to implement a neon sign effect in Flutter. We combined the `Text`, `Stack`, and `Glow` widgets to create a visually appealing neon effect. We also added animation using the `AnimationController` and `Tween` classes to make the glow effect pulsate. With Flutter's versatile widget system, you can further customize and enhance the neon sign effect to fit your application's needs.

Feel free to experiment with different colors, font sizes, and animations to create your unique neon sign effect in Flutter! 🌟

**#Flutter #NeonSignEffect**