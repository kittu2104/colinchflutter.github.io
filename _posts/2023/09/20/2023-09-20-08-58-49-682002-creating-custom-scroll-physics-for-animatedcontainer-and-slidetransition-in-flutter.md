---
layout: post
title: "Creating custom scroll physics for AnimatedContainer and SlideTransition in Flutter"
description: " "
date: 2023-09-20
tags: [customscrollphysics]
comments: true
share: true
---

Flutter provides a rich set of widgets and animations to create visually stunning and interactive user interfaces. Two commonly used widgets are `AnimatedContainer` and `SlideTransition`, which allow us to create smooth animations for moving and resizing widgets on the screen.

However, sometimes we may want more control over the scrolling behavior of these animations. In such cases, we can create custom scroll physics to achieve the desired effects. In this blog post, we will explore how to create custom scroll physics for `AnimatedContainer` and `SlideTransition` in Flutter.

## Custom Scroll Physics for AnimatedContainer

The `AnimatedContainer` widget in Flutter allows us to animate the size, position, and other properties of a container. By default, it uses the physics of its parent scrollable widget. But what if we want to create a bouncing effect when the container reaches the edge of the screen?

To create a custom scroll physics for `AnimatedContainer`, we need to subclass the `ScrollPhysics` class and override the `applyBoundaryConditions` method. Here's an example:

```dart
import 'package:flutter/gestures.dart';
import 'package:flutter/physics.dart';

class BouncingScrollPhysics extends ScrollPhysics {
  const BouncingScrollPhysics({ScrollPhysics parent}) : super(parent: parent);

  @override
  BouncingScrollPhysics applyTo(ScrollPhysics ancestor) {
    return BouncingScrollPhysics(parent: buildParent(ancestor));
  }

  @override
  bool shouldAcceptUserGesture(GestureType gestureType) {
    return false; // Disable user scrolling
  }

  @override
  Simulation createBallisticSimulation(ScrollMetrics position, double velocity) {
    final tolerance = this.tolerance;

    if (velocity.abs() < tolerance.velocity)
      return null;

    return BouncingScrollSimulation(
      spring: SpringDescription.withDampingRatio(
        mass: 1.0,
        stiffness: 500.0,
        ratio: 1.1
      ),
      position: position.pixels,
      velocity: velocity,
      tolerance: tolerance
    );
  }
}
```

In the example above, we create a subclass of `ScrollPhysics` called `BouncingScrollPhysics`. We override the `shouldAcceptUserGesture` method to disable user scrolling and the `createBallisticSimulation` method to create a bouncing scroll simulation using `BouncingScrollSimulation`.

To use our custom scroll physics, we pass it as the `physics` property to the `AnimatedContainer` widget:

```dart
AnimatedContainer(
  duration: Duration(milliseconds: 500),
  width: _isExpanded ? 200 : 100,
  height: _isExpanded ? 200 : 100,
  curve: Curves.easeInOut,
  decoration: BoxDecoration(
    color: Colors.blue,
    borderRadius: BorderRadius.circular(10),
  ),
  child: ...,
  physics: BouncingScrollPhysics(),
)
```

By using our custom `BouncingScrollPhysics`, the `AnimatedContainer` will animate with a bouncing effect when it reaches the edge of the screen.

## Custom Scroll Physics for SlideTransition

The `SlideTransition` widget in Flutter allows us to animate the position of a widget by sliding it from one position to another. By default, it uses the physics of its parent scrollable widget. However, if we want to create a frictionless sliding effect, we can create a custom scroll physics for `SlideTransition`.

Here's an example of creating a custom scroll physics for `SlideTransition`:

```dart
import 'package:flutter/gestures.dart';
import 'package:flutter/physics.dart';

class FrictionlessScrollPhysics extends ScrollPhysics {
  const FrictionlessScrollPhysics({ScrollPhysics parent}) : super(parent: parent);

  @override
  FrictionlessScrollPhysics applyTo(ScrollPhysics ancestor) {
    return FrictionlessScrollPhysics(parent: buildParent(ancestor));
  }

  @override
  bool shouldAcceptUserGesture(GestureType gestureType) {
    return false; // Disable user scrolling
  }

  @override
  Simulation createBallisticSimulation(ScrollMetrics position, double velocity) {
    final tolerance = this.tolerance;

    if (velocity.abs() < tolerance.velocity)
      return null;

    return FrictionSimulation(
      0.1, // Lower friction for a smoother sliding effect
      position.pixels,
      velocity,
      tolerance.velocity,
    );
  }
}
```

In the example above, we create a subclass of `ScrollPhysics` called `FrictionlessScrollPhysics`. We override the `shouldAcceptUserGesture` method to disable user scrolling and the `createBallisticSimulation` method to create a frictionless scroll simulation using `FrictionSimulation`. By adjusting the friction value in `FrictionSimulation`, we can control the smoothness of the sliding effect.

To apply our custom scroll physics to `SlideTransition`, we pass it as the `physics` property to the parent scrollable widget:

```dart
SingleChildScrollView(
  physics: FrictionlessScrollPhysics(),
  child: SlideTransition(
    position: _position,
    child: ...,
  ),
)
```

By using our custom `FrictionlessScrollPhysics`, the child widget of `SlideTransition` will slide smoothly without any friction effect.

## Conclusion

In this blog post, we explored how to create custom scroll physics for `AnimatedContainer` and `SlideTransition` in Flutter. By subclassing `ScrollPhysics` and overriding the necessary methods, we can have more control over the scrolling behavior of these animations. Whether it's creating a bouncing effect for an `AnimatedContainer` or a frictionless sliding effect for a `SlideTransition`, custom scroll physics allow us to achieve the desired visual effects in our Flutter applications.

#flutter #customscrollphysics