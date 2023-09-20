---
layout: post
title: "Implementing custom scroll physics for PageController and PositionedTransition in Flutter"
description: " "
date: 2023-09-20
tags: []
comments: true
share: true
---

In Flutter, the `PageController` and `PositionedTransition` are two commonly used widgets for creating dynamic and animated UI. However, by default, they use the built-in physics for scrolling and transitioning. In some cases, you may want to implement custom scroll physics to achieve a specific scrolling behavior. In this blog post, we will explore how to implement custom scroll physics for `PageController` and `PositionedTransition`.

## Custom scroll physics for PageController

`PageController` is used for controlling a `PageView`. By default, it uses `AlwaysScrollableScrollPhysics`, which allows for infinite scrolling in both directions. To implement custom scroll physics, we can create a new class that extends `ScrollPhysics` and override its methods.

```dart
class CustomPageScrollPhysics extends ScrollPhysics {
  const CustomPageScrollPhysics({ScrollPhysics parent}) : super(parent: parent);

  @override
  CustomPageScrollPhysics applyTo(ScrollPhysics ancestor) {
    return CustomPageScrollPhysics(parent: buildParent(ancestor));
  }

  @override
  double get minFlingVelocity => 800.0;

  @override
  double get maxFlingVelocity => 8000.0;

  @override
  Simulation createBallisticSimulation(
      ScrollMetrics position, double velocity) {
    final double pixelsPerSecond = velocity.abs() * 0.25;
    return ScrollSpringSimulation(
      spring,
      position.pixels,
      position.maxScrollExtent,
      -pixelsPerSecond,
      tolerance: tolerance,
    );
  }
}
```

In the `CustomPageScrollPhysics` class, we override the `minFlingVelocity`, `maxFlingVelocity`, and `createBallisticSimulation` methods to customize the physics. In this example, we set the minimum and maximum fling velocities to 800.0 and 8000.0 respectively, and use a `ScrollSpringSimulation` for the ballistic simulation.

To use the custom scroll physics with `PageController`, simply pass it as the `physics` parameter when creating the `PageView`:

```dart
PageView(
  controller: PageController(),
  physics: const CustomPageScrollPhysics(),
  ...
)
```

## Custom scroll physics for PositionedTransition

`PositionedTransition` is used for animating the position of a widget within a `Stack`. By default, it uses `ClampingScrollPhysics`, which limits the scrollable range. To implement custom scroll physics, we can create a new class that extends `ScrollPhysics` and override its methods in a similar way as before.

```dart
class CustomPositionedScrollPhysics extends ScrollPhysics {
  const CustomPositionedScrollPhysics({ScrollPhysics parent}) : super(parent: parent);

  @override
  CustomPositionedScrollPhysics applyTo(ScrollPhysics ancestor) {
    return CustomPositionedScrollPhysics(parent: buildParent(ancestor));
  }

  @override
  double get minFlingVelocity => 500.0;

  @override
  double get maxFlingVelocity => 5000.0;

  @override
  Simulation createBallisticSimulation(
      ScrollMetrics position, double velocity) {
    final double pixelsPerSecond = velocity.abs() * 0.3;
    return ScrollSpringSimulation(
      spring,
      position.pixels,
      position.maxScrollExtent,
      -pixelsPerSecond,
      tolerance: tolerance,
    );
  }
}
```

In the `CustomPositionedScrollPhysics` class, we again override the `minFlingVelocity`, `maxFlingVelocity`, and `createBallisticSimulation` methods to customize the physics. In this example, we set the minimum and maximum fling velocities to 500.0 and 5000.0 respectively, and use a `ScrollSpringSimulation` for the ballistic simulation.

To use the custom scroll physics with `PositionedTransition`, simply pass it as the `scrollPhysics` parameter when creating the `PositionedTransition`:

```dart
PositionedTransition(
  position: animation.drive(
    Tween<Offset>(
      begin: Offset.zero,
      end: Offset(1.0, 0),
    ),
  ),
  scrollPhysics: const CustomPositionedScrollPhysics(),
  child: ...
)
```

By implementing custom scroll physics for `PageController` and `PositionedTransition`, you can achieve unique and specific scrolling behaviors in your Flutter applications.