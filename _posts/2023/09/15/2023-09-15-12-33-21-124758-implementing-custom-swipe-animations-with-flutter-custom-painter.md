---
layout: post
title: "Implementing custom swipe animations with Flutter Custom Painter"
description: " "
date: 2023-09-15
tags: [customanimation]
comments: true
share: true
---

Swipe gestures have become an essential part of modern mobile app interfaces. Flutter, being a powerful and flexible UI framework, allows us to implement custom swipe animations using the `CustomPainter` class.

In this tutorial, we will explore how to create a custom swipe animation in Flutter using `CustomPainter`. We will create a simple swipe gesture that moves a widget from left to right.

To get started, create a new Flutter project and open the main.dart file. 

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Swipe Animation',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: SwipeScreen(),
    );
  }
}

class SwipeScreen extends StatefulWidget {
  @override
  _SwipeScreenState createState() => _SwipeScreenState();
}

class _SwipeScreenState extends State<SwipeScreen> with TickerProviderStateMixin {
  AnimationController _controller;
  
  @override
  void initState() {
    _controller = AnimationController(
      vsync: this,
      duration: Duration(milliseconds: 500),
    )
    ..addListener(() {
      setState(() {});
    });
    super.initState();
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    double xOffset = 0.0;
    double screenWidth = MediaQuery.of(context).size.width;
    double screenHeight = MediaQuery.of(context).size.height;
    
    return GestureDetector(
      onHorizontalDragUpdate: (DragUpdateDetails details) {
        xOffset += details.delta.dx;
        if (xOffset > 0) {
          _controller.value = xOffset / screenWidth;
        }
        setState(() {});
      },
      onHorizontalDragEnd: (DragEndDetails details) {
        if (_controller.isAnimating || _controller.status == AnimationStatus.completed) return;
        if (_controller.value > 0.5) {
          _controller.fling(velocity: 2.0);
        } else {
          _controller.reverse();
        }
      },
      child: Scaffold(
        body: CustomPaint(
          painter: SwipePainter(
            swipeOffset: xOffset,
            screenWidth: screenWidth,
            screenHeight: screenHeight,
          ),
          child: Container(
            color: Colors.white,
            child: Center(
              child: Text(
                'Swipe me!',
                style: TextStyle(fontSize: 24),
              ),
            ),
          ),
        ),
      ),
    );
  }
}

class SwipePainter extends CustomPainter {
  final double swipeOffset;
  final double screenWidth;
  final double screenHeight;

  SwipePainter({
    this.swipeOffset,
    this.screenWidth,
    this.screenHeight,
  });

  @override
  void paint(Canvas canvas, Size size) {
    double circleRadius = 50.0;
    double circleX = swipeOffset + circleRadius;
    double circleY = screenHeight / 2;
    
    canvas.drawCircle(
      Offset(circleX, circleY),
      circleRadius,
      Paint()..color = Colors.blue,
    );
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    return true;
  }
}
```

Let's go through the code. First, we start by defining our main function and MyApp stateless widget. In the `MyApp` widget, we set the app title and its theme, and then set the home screen to `SwipeScreen`.

In `SwipeScreen`, we use the `TickeProviderStateMixin` for animation purposes. Inside the `_SwipeScreenState` class, we initialize an animation controller that will help us animate the swipe gestures. We also define the `initState` and `dispose` methods to properly set up and clean up the animation controller.

In the `build` method, we define some variables to hold the offset value of the swipe gesture, as well as the screen width and height. We then use a `GestureDetector` widget to handle the swipe gestures. We update the `xOffset` value on horizontal drag updates and update the animation controller accordingly. On horizontal drag end, we check if the animation controller is already animating or completed, and if not, we determine whether to fling or reverse the animation based on the swipe offset value.

The `SwipePainter` class is responsible for drawing the swipe animation on the canvas. In the `paint` method, we calculate the x and y coordinates of the circle to be drawn based on the swipe offset value. We then use `canvas.drawCircle` to draw the circle on the canvas.

Finally, we wrap the `Scaffold` with a `CustomPaint` widget and pass in the `SwipePainter` as the painter. Inside the `Container`, we display a simple text widget with the instruction "Swipe me!".

That's it! Now you can run your app and start swiping the widget from left to right. You can customize and extend this example to create more complex swipe animations based on your app's requirements.

#flutter #customanimation