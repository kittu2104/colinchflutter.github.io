---
layout: post
title: "How to use the SizeTransition widget with the Opacity widget for fade-in and size animations"
description: " "
date: 2023-09-25
tags: [Flutter, Animations]
comments: true
share: true
---

In Flutter, you can create beautiful animations using various built-in widgets. Two powerful widgets that can be combined for fade-in and size animations are the `SizeTransition` and `Opacity` widgets.

The `SizeTransition` widget allows you to animate the size of a child widget, while the `Opacity` widget controls the opacity or transparency of its child widget. By combining these two widgets, you can create a fade-in effect along with a change in size.

Here's an example code snippet demonstrating how to use these widgets together:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage>
    with SingleTickerProviderStateMixin {
  AnimationController _animationController;
  Animation<double> _fadeAnimation;
  Animation<double> _sizeAnimation;

  @override
  void initState() {
    super.initState();

    _animationController = AnimationController(
      vsync: this,
      duration: Duration(seconds: 2),
    );

    _fadeAnimation = Tween<double>(begin: 0, end: 1).animate(_animationController);

    _sizeAnimation = Tween<double>(begin: 100, end: 200).animate(
      CurvedAnimation(
        parent: _animationController,
        curve: Curves.easeInOut,
      ),
    );
    
    _animationController.forward();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Fade-in and Size Animation'),
      ),
      body: Center(
        child: AnimatedBuilder(
          animation: _animationController,
          builder: (BuildContext context, Widget child) {
            return SizeTransition(
              sizeFactor: _sizeAnimation,
              child: Opacity(
                opacity: _fadeAnimation.value,
                child: Container(
                  width: 100,
                  height: 100,
                  color: Colors.blue,
                ),
              ),
            );
          },
        ),
      ),
    );
  }

  @override
  void dispose() {
    _animationController.dispose();
    super.dispose();
  }
}
```

In this example, the `SizeTransition` widget is used to animate the size of the `Container` widget, and the `Opacity` widget is used to animate its fade-in effect. The animations are controlled by an `AnimationController` and its associated animations.

By tweaking the values of the `Tween` and `CurvedAnimation`, you can customize the animations according to your requirements.

Remember to dispose of the `AnimationController` in the `dispose()` method to avoid any memory leaks.

With this approach, you can easily create fade-in and size animations using the `SizeTransition` and `Opacity` widgets in Flutter.

#Flutter #Animations