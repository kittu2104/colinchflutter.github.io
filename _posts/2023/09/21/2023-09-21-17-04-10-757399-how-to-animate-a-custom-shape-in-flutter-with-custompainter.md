---
layout: post
title: "How to animate a custom shape in Flutter with CustomPainter"
description: " "
date: 2023-09-21
tags: [flutter, animation]
comments: true
share: true
---

Animating a custom shape in Flutter can be achieved by using the `CustomPainter` class. `CustomPainter` allows you to create your own shapes and paint them on the screen. To animate these shapes, you can use the `AnimationController` along with a `CustomPainter` and update the values of the shape's properties over time.

## Step 1: Create a Custom Shape

First, create a custom shape by extending the `CustomPainter` class and overriding the `paint` and `shouldRepaint` methods.

```dart
class CustomShape extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // Define the shape's properties and draw it on the canvas
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    // Return true if the shape needs to be repainted or false otherwise
  }
}
```

In the `paint` method, you can use the `Canvas` object to draw your custom shape using methods like `drawRect`, `drawCircle`, or `drawPath`. The `size` parameter specifies the available space to draw the shape.

In the `shouldRepaint` method, you determine whether the shape needs to be repainted. Return `true` if the shape's properties have changed and need to be redrawn, or `false` if the shape remains the same.

## Step 2: Create an Animation Controller

Next, create an `AnimationController` instance to control the animation. This controller will be used to define the duration and the value range of the animation.

```dart
class MyWidget extends StatefulWidget {
  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> with SingleTickerProviderStateMixin {
  late AnimationController _controller;

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: Duration(seconds: 1),
      vsync: this,
    );
    _controller.forward();
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Container(
      // Your widget code here
    );
  }
}
```

The `AnimationController` needs to be provided with a `TickerProvider` that manages the timing of the animation. In the example above, the `SingleTickerProviderStateMixin` mixin is used to provide a `vsync` argument for the animation controller.

## Step 3: Animate the Custom Shape

To animate the custom shape, you can use the `Animation` object provided by the `AnimationController`. By animating the properties of the shape within a `setState` method, you can trigger the repainting of the custom shape at each frame.

```dart
class _MyWidgetState extends State<MyWidget> with SingleTickerProviderStateMixin {
  late AnimationController _controller;
  late Animation<double> _animation;

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: Duration(seconds: 1),
      vsync: this,
    );
    _animation = Tween<double>(begin: 0.0, end: 1.0).animate(_controller);
    _controller.forward();
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Container(
      child: AnimatedBuilder(
        animation: _animation,
        builder: (context, child) {
          return CustomPaint(
            painter: CustomShape(),
            size: Size(200, 200),
          );
        },
      ),
    );
  }
}
```

In the example above, the `_animation` variable is defined using the `Tween` class to interpolate between the start and end values of the animation. The `CustomPaint` widget is wrapped inside an `AnimatedBuilder`, which rebuilds the widget tree whenever `_animation` updates. This triggers the repainting of the custom shape.

## Conclusion

Animating a custom shape in Flutter with `CustomPainter` allows you to create visually appealing and interactive animations. By leveraging the power of `AnimationController` and `Animation`, you can bring your custom shapes to life. Experiment with different shapes and animation properties to create your own unique effects.

#flutter #animation