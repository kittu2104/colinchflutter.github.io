---
layout: post
title: "How to use the Opacity widget with the AnimatedBuilder widget for custom opacity animations"
description: " "
date: 2023-09-25
tags: [flutter, flutteranimation]
comments: true
share: true
---

Opacity animation is a common requirement in many user interfaces. Flutter provides the `AnimatedBuilder` widget to achieve custom animations. When combined with the `Opacity` widget, you can create sophisticated opacity animations easily.

In this tutorial, we will demonstrate how to use the `Opacity` widget with the `AnimatedBuilder` widget to create custom opacity animations in Flutter.

## Step 1: Create a StatefulWidget

First, let's create a new `StatefulWidget` called `OpacityAnimation`. This widget will hold the state and manage the opacity value.

```dart
class OpacityAnimation extends StatefulWidget {
  @override
  _OpacityAnimationState createState() => _OpacityAnimationState();
}

class _OpacityAnimationState extends State<OpacityAnimation> {
  double _opacity = 0.0;

  @override
  Widget build(BuildContext context) {
    return Container(
      child: AnimatedBuilder(
        animation: Tween<double>(begin: 0.0, end: 1.0).animate(
          CurvedAnimation(
            parent: widget.controller,
            curve: Curves.easeIn,
          ),
        ),
        builder: (BuildContext context, Widget child) {
          return Opacity(
            opacity: _opacity,
            child: child,
          );
        },
        child: Text('Hello, Opacity Animation!'),
      ),
    );
  }
}
```

In the code above, we define the `_opacity` variable to hold the opacity value. We use the `AnimatedBuilder` widget to listen to the animation updates and rebuild the widget tree accordingly. Inside the builder function, we wrap the child widget with the `Opacity` widget, passing the `_opacity` value as the opacity value.

## Step 2: Create an Animation Controller

Next, let's create an `AnimationController` in the parent widget to control the animation.

```dart
class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage>
    with SingleTickerProviderStateMixin {
  late AnimationController _animationController;

  @override
  void initState() {
    super.initState();
    _animationController = AnimationController(
      duration: Duration(seconds: 2),
      vsync: this,
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
      appBar: AppBar(
        title: Text('Opacity Animation'),
      ),
      body: OpacityAnimation(controller: _animationController),
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

In the above code, we create an `_animationController` object in the parent widget's `initState()` method and dispose of it in the `dispose()` method. We pass the `_animationController` object to the `OpacityAnimation` widget as a parameter.

## Step 3: Test the Animation

To see the opacity animation in action, run the app and press the "Play" button on the floating action button. The child widget inside the `OpacityAnimation` widget will fade in with a smooth opacity animation.

That's it! You have successfully used the `Opacity` widget with the `AnimatedBuilder` widget to create custom opacity animations in Flutter.

# Conclusion

Using the `Opacity` widget with the `AnimatedBuilder` widget provides a powerful way to create custom opacity animations in Flutter. By adjusting the `_opacity` variable and controlling the animation using an `AnimationController`, you can create various opacity effects to enhance your UI. Play around with different values and curves to achieve the desired animated opacity effect.

#flutter #flutteranimation