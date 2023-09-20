---
layout: post
title: "Designing custom scroll physics for SliverAppBar and SliverFillRemaining in Flutter"
description: " "
date: 2023-09-20
tags: [Flutter, ScrollPhysics]
comments: true
share: true
---

In Flutter, widgets like `SliverAppBar` and `SliverFillRemaining` provide flexible and customizable scrolling behavior. However, the default scroll physics might not always meet your specific requirements. In such cases, you can design your own custom scroll physics to achieve the desired scrolling effect. In this blog post, we will explore how to create custom scroll physics for `SliverAppBar` and `SliverFillRemaining`.

## What are Scroll Physics?

Scroll physics determine how a scrollable widget, such as a `ListView` or `GridView`, behaves when the user scrolls or flings. The physics define properties like the scroll position, velocity, and the behavior when reaching the scroll boundaries. By creating custom scroll physics, you can tailor the scrolling behavior to your app's needs.

## Custom Scroll Physics for `SliverAppBar`

To create custom scroll physics for `SliverAppBar`, you need to extend the `ScrollPhysics` class and override the relevant methods. Let's see an example where we want the app bar to be "sticky" and remain at the top until the user scrolls a certain distance:

```dart
class StickyScrollPhysics extends ScrollPhysics {
  StickyScrollPhysics({ScrollPhysics parent}) : super(parent: parent);

  @override
  StickyScrollPhysics applyTo(ScrollPhysics ancestor) {
    return StickyScrollPhysics(parent: buildParent(ancestor));
  }

  @override
  double applyPhysicsToUserOffset(ScrollMetrics position, double offset) {
    final double overscrollPastLeadingExtent = _calculateOverscrollPastLeadingExtent(position);
    final double overscrollPastTrailingExtent = _calculateOverscrollPastTrailingExtent(position);

    final double overscrollExtent = math.max(
      overscrollPastLeadingExtent,
      overscrollPastTrailingExtent,
    );

    final double overscrollBoundary = position.viewportDimension * 0.4;
    final double correctionOffset = overscrollExtent > overscrollBoundary ? 0.0 : offset;

    return super.applyPhysicsToUserOffset(position, correctionOffset);
  }

  double _calculateOverscrollPastLeadingExtent(ScrollMetrics position) {
    return (position.minScrollExtent - position.pixels).clamp(0, double.infinity);
  }

  double _calculateOverscrollPastTrailingExtent(ScrollMetrics position) {
    return (position.pixels - position.maxScrollExtent).clamp(0, double.infinity);
  }
}
```

Here, we extend `ScrollPhysics` and override the `applyPhysicsToUserOffset` method. We calculate the overscroll past leading and trailing extents and compare them to a defined threshold. If the overscroll exceeds the threshold, we correct the offset to prevent the app bar from sticking.

To use this custom scroll physics with `SliverAppBar`, you can wrap it within a `CustomScrollView` using the `physics` property:

```dart
CustomScrollView(
  physics: StickyScrollPhysics(),
  slivers: [
    SliverAppBar(
      //...your app bar configurations
    ),
    //...other sliver widgets
  ],
)
```

## Custom Scroll Physics for `SliverFillRemaining`

Similarly, you can create custom scroll physics for `SliverFillRemaining` by extending `ScrollPhysics`. Let's consider an example where we want to prevent overscrolling past the remaining sliver:

```dart
class NoOverscrollPhysics extends ScrollPhysics {
  NoOverscrollPhysics({ScrollPhysics parent}) : super(parent: parent);

  @override
  NoOverscrollPhysics applyTo(ScrollPhysics ancestor) {
    return NoOverscrollPhysics(parent: buildParent(ancestor));
  }

  @override
  double applyBoundaryConditions(ScrollMetrics position, double value) {
    double result = super.applyBoundaryConditions(position, value);
    if (position.outOfRange && value < position.pixels && position.pixels <= position.maxScrollExtent) {
      result = position.pixels - value;
    }
    return result;
  }
}
```

Here, we override the `applyBoundaryConditions` method to prevent overscrolling when the remaining sliver is reached. If the position is out of range, we calculate the difference between the current position and the target position, and limit the scroll accordingly.

To apply this custom scroll physics to `SliverFillRemaining`, you can use the `physics` property of `CustomScrollView`:

```dart
CustomScrollView(
  physics: NoOverscrollPhysics(),
  slivers: [
    //...other slivers
    SliverFillRemaining(
      //...your widget configurations
    ),
  ],
)
```

## Conclusion

By creating custom scroll physics for `SliverAppBar` and `SliverFillRemaining`, you can add unique scrolling behaviors to your Flutter app. Experiment with different scroll physics parameters and behaviors to enhance the user experience. Harness the power of Flutter's flexible and customizable widgets to create stunning scrolling effects in your app!

\#Flutter #ScrollPhysics #Customization