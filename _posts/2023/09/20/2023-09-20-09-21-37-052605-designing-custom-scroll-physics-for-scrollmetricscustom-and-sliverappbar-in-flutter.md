---
layout: post
title: "Designing custom scroll physics for ScrollMetrics.custom and SliverAppBar in Flutter"
description: " "
date: 2023-09-20
tags: [Flutter, ScrollPhysics]
comments: true
share: true
---

Scroll physics in Flutter determine how a scrollable widget responds to user interactions, such as flicks or drags. By default, Flutter provides several pre-defined scroll physics, but you can also design custom scroll physics to achieve specific scroll behavior.

## ScrollPhysics Overview

Scroll physics in Flutter are represented by `ScrollPhysics` class and its subclasses. The base `ScrollPhysics` class handles basic physics calculations, while the subclasses refine the behavior further.

To design custom scroll physics, you can extend the `ScrollPhysics` class and override its methods to control the physics calculations.

## Extending ScrollPhysics

Here's an example of extending `ScrollPhysics` to create custom scroll physics for `ScrollMetrics.custom` and `SliverAppBar` in Flutter:

```dart
class CustomScrollPhysics extends ScrollPhysics {
  final double overscrollDistance;

  CustomScrollPhysics({this.overscrollDistance, ScrollPhysics parent})
      : super(parent: parent);

  @override
  double applyBoundaryConditions(ScrollMetrics position, double value) {
    double extentLimit = position.extentInside;
    double deltaLimit = overscrollDistance;

    if (value < position.pixels && position.pixels <= 0.0) {
      return value - position.pixels;
    } else if (value > extentLimit && position.pixels >= extentLimit - deltaLimit) {
      return value - (position.pixels - (extentLimit - deltaLimit));
    }

    return 0.0;
  }

  @override
  ScrollPhysics applyTo(ScrollPhysics ancestor) {
    return CustomScrollPhysics(
      overscrollDistance: overscrollDistance,
      parent: buildParent(ancestor),
    );
  }
}
```

In the code above, we have created a custom scroll physics class called `CustomScrollPhysics`. It takes an additional parameter `overscrollDistance`, which represents the maximum distance allowed for overscrolling.

The `applyBoundaryConditions` method is overridden to apply custom boundary conditions when scrolling. We check if the scroll position goes beyond the scrollable extents and adjust the scroll position accordingly.

The `applyTo` method is overridden so that the custom scroll physics can be reused with other scroll physics. This is useful when integrating with other widgets, like `NestedScrollView` or `CustomScrollView`.

## Using CustomScrollPhysics

To use the custom scroll physics, you can simply pass an instance of `CustomScrollPhysics` to the scrollable widget's `physics` property.

For example, if you are using `ScrollView` widget:

```dart
ScrollView(
  physics: CustomScrollPhysics(overscrollDistance: 100.0),
  // ...
)
```

Or, if you are using `CustomScrollView` widget:

```dart
CustomScrollView(
  physics: CustomScrollPhysics(overscrollDistance: 100.0).applyTo(BouncingScrollPhysics()),
  // ...
)
```

In the above examples, we set `overscrollDistance` to `100.0` as an example. You can adjust it to fit your specific needs.

## Conclusion

Designing custom scroll physics allows you to have full control over the scrolling behavior in Flutter. By extending the `ScrollPhysics` class and overriding its methods, you can craft scroll physics that suit the requirements of your app.

By providing a custom implementation, you can achieve unique scrolling effects and enhance the user experience. So go ahead, customize your scroll physics and make your app stand out!

#Flutter #ScrollPhysics