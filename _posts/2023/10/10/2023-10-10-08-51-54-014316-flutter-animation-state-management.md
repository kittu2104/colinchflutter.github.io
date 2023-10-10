---
layout: post
title: "Flutter animation state management"
description: " "
date: 2023-10-10
tags: [animation]
comments: true
share: true
---

When building animations in Flutter, one important aspect to consider is how to manage the animation state. Flutter provides various approaches to handle animation state management, each with its own benefits and use cases. In this article, we will explore some of the popular options available.

## 1. `setState` method

The simplest way to manage animation state in Flutter is by using the `setState` method. This method is commonly used with `AnimatedBuilder` widget to rebuild the widget tree whenever the animation state changes. Inside the `setState`, you update the animation values and trigger a rebuild of the widget tree.

```dart
class AnimatedWidgetExample extends StatefulWidget {
  @override
  _AnimatedWidgetExampleState createState() => _AnimatedWidgetExampleState();
}

class _AnimatedWidgetExampleState extends State<AnimatedWidgetExample>
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

    _animation = Tween<double>(begin: 0, end: 1).animate(_controller);
    _controller.forward();
  }

  @override
  Widget build(BuildContext context) {
    return AnimatedBuilder(
      animation: _animation,
      builder: (BuildContext context, Widget child) {
        return Opacity(
          opacity: _animation.value,
          child: child,
        );
      },
      child: Container(
        width: 200,
        height: 200,
        color: Colors.blue,
      ),
    );
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }
}
```

## 2. `AnimationController` with `addListener`

Another approach to manage animation state is by using the `AnimationController` along with the `addListener` method. Here, you manually update the animation values inside the listener every time the animation state changes. This gives you more control over the animation, as you can perform additional operations based on the animation values.

```dart
class AnimationControllerExample extends StatefulWidget {
  @override
  _AnimationControllerExampleState createState() =>
      _AnimationControllerExampleState();
}

class _AnimationControllerExampleState extends State<AnimationControllerExample>
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

    _animation = Tween<double>(begin: 0, end: 1).animate(_controller);
    _animation.addListener(() {
      setState(() {}); // Rebuild the widget tree
    });
    _controller.forward();
  }

  @override
  Widget build(BuildContext context) {
    return Opacity(
      opacity: _animation.value,
      child: Container(
        width: 200,
        height: 200,
        color: Colors.blue,
      ),
    );
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }
}
```

## 3. Provider Package

If your animation state needs to be shared across multiple widgets, you can consider using the `provider` package. The `provider` package provides a convenient way to manage state and efficiently rebuild only the widgets that depend on the state.

```dart
class AnimationProviderExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ChangeNotifierProvider(
      create: (context) => AnimationState(),
      child: Consumer<AnimationState>(
        builder: (context, animState, child) {
          return Opacity(
            opacity: animState.animationValue,
            child: Container(
              width: 200,
              height: 200,
              color: Colors.blue,
            ),
          );
        },
      ),
    );
  }
}

class AnimationState extends ChangeNotifier {
  AnimationController _controller;
  Animation<double> _animation;

  AnimationState() {
    _controller = AnimationController(
      duration: Duration(seconds: 2),
      vsync: this,
    );

    _animation = Tween<double>(begin: 0, end: 1).animate(_controller);
    _controller.forward();
  }

  double get animationValue => _animation.value;

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }
}
```

These are just a few examples of how to manage animation state in Flutter. Choose the approach that best suits your project requirements and complexity. Remember to consider factors such as widget tree hierarchy, shared state, and performance to ensure smooth and efficient animations in your Flutter applications.

# Conclusion

In this article, we explored different methods to manage animation state in Flutter. We looked at using `setState`, `AnimationController` with `addListener`, and the `provider` package. Each method has its own advantages and use cases, so choose the one that works best for your specific needs. By effectively managing animation state, you can create engaging and visually appealing animations in your Flutter apps.

## Related Hashtags

#flutter #animation