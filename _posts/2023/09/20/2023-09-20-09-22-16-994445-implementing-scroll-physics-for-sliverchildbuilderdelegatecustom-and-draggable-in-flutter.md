---
layout: post
title: "Implementing scroll physics for SliverChildBuilderDelegate.custom and Draggable in Flutter"
description: " "
date: 2023-09-20
tags: []
comments: true
share: true
---

In Flutter, scrollable widgets provide a way to scroll or slide through a set of child widgets. Two commonly used scrollable widgets are `SliverChildBuilderDelegate.custom` and `Draggable`.

## Scroll Physics in Flutter

Scroll physics determine how a scrollable widget behaves when the user interacts with it. Flutter provides several built-in scroll physics classes, such as `ClampingScrollPhysics`, `BouncingScrollPhysics`, and `AlwaysScrollableScrollPhysics`. However, there might be cases where you need to implement custom scroll physics to achieve specific behavior.

## SliverChildBuilderDelegate.custom

The `SliverChildBuilderDelegate.custom` constructor is used with a `CustomScrollView` to lazily build children for a sliver list. When using `SliverChildBuilderDelegate.custom`, you can define custom scroll physics by extending the `ScrollPhysics` class and overriding its methods.

Here's an example of implementing custom scroll physics for `SliverChildBuilderDelegate.custom`:

```dart
class CustomScrollPhysics extends ScrollPhysics {
  const CustomScrollPhysics({ScrollPhysics? parent}) : super(parent: parent);

  @override
  CustomScrollPhysics applyTo(ScrollPhysics? ancestor) {
    return CustomScrollPhysics(parent: buildParent(ancestor));
  }

  @override
  double getPixels(ScrollMetrics position, double velocity) {
    // Implement desired behavior for scrolling pixels
    // based on position and velocity.
    return super.getPixels(position, velocity);
  }

  @override
  double applyPhysicsToUserOffset(ScrollMetrics position, double offset) {
    // Implement desired behavior for applying scroll physics
    // to user offsets.
    return super.applyPhysicsToUserOffset(position, offset);
  }

  // Override other ScrollPhysics methods as needed.
}
```

To use the custom scroll physics with `SliverChildBuilderDelegate.custom`, you can pass an instance of `CustomScrollPhysics` as the `physics` parameter:

```dart
CustomScrollView(
  physics: const CustomScrollPhysics(),
  slivers: [
    SliverList(
      delegate: SliverChildBuilderDelegate.custom(
        (BuildContext context, int index) {
          // Build and return child widget.
        },
        childCount: itemCount,
      ),
    ),
  ],
)
```

## Draggable in Flutter

The `Draggable` widget provides drag-and-drop functionality in Flutter. By default, it uses `ScrollablePhysics` as the physics for scrolling when dragging an item. However, you can override the default scroll physics to achieve custom behavior while dragging.

Here's an example of implementing custom scroll physics for a `Draggable` widget:

```dart
class CustomScrollPhysics extends ScrollPhysics {
  const CustomScrollPhysics({ScrollPhysics? parent}) : super(parent: parent);

  @override
  CustomScrollPhysics applyTo(ScrollPhysics? ancestor) {
    return CustomScrollPhysics(parent: buildParent(ancestor));
  }

  @override
  double getPixels(ScrollMetrics position, double velocity) {
    // Implement desired behavior for scrolling pixels
    // based on position and velocity.
    return super.getPixels(position, velocity);
  }

  @override
  double applyPhysicsToUserOffset(ScrollMetrics position, double offset) {
    // Implement desired behavior for applying scroll physics
    // to user offsets.
    return super.applyPhysicsToUserOffset(position, offset);
  }

  // Override other ScrollPhysics methods as needed.
}

// Custom Draggable
class CustomDraggable extends Draggable {
  const CustomDraggable({
    Key? key,
    required Widget child,
    required DragAnchor? feedback,
    DragAnchor? childWhenDragging,
    Axis? axis,
    Widget? feedbackOffset,
    int? maxSimultaneousDrags,
    Offset? initialChildSize,
    bool? ignoringFeedbackSemantics,
    Axis? scrollDirection,
    ScrollController? scrollController,
    ScrollPhysics? scrollPhysics,
    DraggingStartedFeedbackCallback? onDragStarted,
    DraggingFeedbackCallback? onDraggableCanceled,
    VoidCallback? onDragCompleted,
    Widget? feedbackBuilder,
  }) : super(
          key: key,
          child: child,
          feedback: feedback,
          childWhenDragging: childWhenDragging,
          axis: axis,
          feedbackOffset: feedbackOffset,
          maxSimultaneousDrags: maxSimultaneousDrags,
          initialChildSize: initialChildSize,
          ignoringFeedbackSemantics: ignoringFeedbackSemantics,
          scrollDirection: scrollDirection,
          scrollController: scrollController,
          scrollPhysics: const CustomScrollPhysics(), // Override scroll physics
          onDragStarted: onDragStarted,
          onDraggableCanceled: onDraggableCanceled,
          onDragCompleted: onDragCompleted,
          feedbackBuilder: feedbackBuilder,
        );
}

```

In the above example, we've extended the `ScrollPhysics` class to create custom scroll physics, and used it with both `SliverChildBuilderDelegate.custom` and `Draggable` widgets.

Remember to replace the `CustomScrollPhysics` with your specific scroll physics implementation.

By implementing custom scroll physics, you can fine-tune the behavior of `SliverChildBuilderDelegate.custom` and `Draggable` in Flutter according to your specific requirements.