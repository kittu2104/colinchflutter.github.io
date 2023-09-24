---
layout: post
title: "Implementing custom animations in a StatelessWidget in Flutter"
description: " "
date: 2023-09-24
tags: [flutter, animations]
comments: true
share: true
---

Flutter provides powerful tools for creating stunning and engaging user interfaces, and one such tool is the ability to create custom animations. In this blog post, we will explore how to implement custom animations in a `StatelessWidget` in Flutter.

## Prerequisites
Before we begin, make sure you have Flutter installed on your machine and have a basic understanding of Flutter concepts.

## Let's get started!
To implement custom animations in a `StatelessWidget`, we need to use the `AnimatedBuilder` widget. This widget takes an animation and a builder function as parameters, allowing us to control our animation using a value from 0 to 1.

Here's an example of implementing a fade animation using a `StatelessWidget`:

```dart
class FadeAnimation extends StatelessWidget {
  final AnimationController animationController;

  const FadeAnimation({required this.animationController});

  @override
  Widget build(BuildContext context) {
    return AnimatedBuilder(
      animation: animationController,
      builder: (context, child) {
        return Opacity(
          opacity: animationController.value,
          child: child,
        );
      },
      child: SomeChildWidget(),
    );
  }
}
```

In the above code, we create a `FadeAnimation` widget that takes an `AnimationController` as a parameter. We then use the `AnimatedBuilder`, which rebuilds whenever the `animationController` value changes. Inside the builder function, we set the opacity of the child widget based on the current value of the `animationController`.

To use this `FadeAnimation` widget, you will need to create and control an instance of `AnimationController`, which you can do in the parent widget. Here's an example of how you can use the `FadeAnimation` widget:

```dart
class MyWidget extends StatefulWidget {
  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget>
    with SingleTickerProviderStateMixin {
  late AnimationController _animationController;

  @override
  void initState() {
    super.initState();
    _animationController = AnimationController(
      vsync: this,
      duration: Duration(seconds: 1),
    );
  }

  @override
  void dispose() {
    _animationController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: FadeAnimation(animationController: _animationController),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          _animationController.forward();
        },
        child: Icon(Icons.play_arrow),
      ),
    );
  }
}
```

In this example, we create a `MyWidget` that is a `StatefulWidget` and uses the `FadeAnimation` widget inside its `build` method. We initialize the `AnimationController` in the `initState` method, forward the animation in the `onPressed` callback of the floating action button, and dispose of the `AnimationController` in the `dispose` method.

## Conclusion
By using the `AnimatedBuilder` widget, we can easily create custom animations in a `StatelessWidget` in Flutter. This gives us the flexibility to create engaging UIs with sophisticated animations.

#flutter #animations