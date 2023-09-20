---
layout: post
title: "Creating custom scroll physics for Draggable in Flutter"
description: " "
date: 2023-09-20
tags: [flutter, Draggable]
comments: true
share: true
---

In Flutter, the `Draggable` widget is commonly used for implementing drag and drop functionality. By default, it uses the `ScrollPhysics` class for handling scrolling behavior. However, there might be cases where you need to customize the scrolling physics to achieve a specific behavior.

In this tutorial, we will explore how to create custom scroll physics for the `Draggable` widget in Flutter. We will create a simple example where the draggable item will have a custom scroll physics that limits its movement within a specified range.

Let's get started!

## Step 1: Create a ScrollPhysics subclass

To create custom scroll physics, we need to create a subclass of the `ScrollPhysics` class. This subclass will override the necessary methods to define the desired behavior.

Here's an example of a custom scroll physics class that limits the draggable item's movement within a specific range:

```dart
class CustomScrollPhysics extends ScrollPhysics {
  final double rangeStart;
  final double rangeEnd;

  const CustomScrollPhysics({ScrollPhysics? parent, required this.rangeStart, required this.rangeEnd})
      : super(parent: parent);

  @override
  CustomScrollPhysics applyTo(ScrollPhysics? ancestor) {
    return CustomScrollPhysics(parent: buildParent(ancestor), rangeStart: rangeStart, rangeEnd: rangeEnd);
  }

  @override
  double applyBoundaryConditions(ScrollMetrics? position, double value) {
    if (value < rangeStart)
      return rangeStart;
    else if (value > rangeEnd)
      return rangeEnd;
    return super.applyBoundaryConditions(position, value);
  }

  @override
  Simulation? createBallisticSimulation(ScrollMetrics? position, double velocity) {
    final range = rangeEnd - rangeStart;
    final tolerance = tolerance.velocity;
    if (position!.outOfRange) {
      return ScrollSpringSimulation(
        spring,
        position.pixels,
        position.minScrollExtent,
        position.maxScrollExtent,
        tolerance: tolerance,
      );
    }
    if (velocity.abs() < tolerance.velocity)
      return null;

    return ScrollSpringSimulation(
      spring,
      position.pixels,
      position.pixels + velocity.clamp(-range, range),
      position.maxScrollExtent,
      tolerance: tolerance,
    );
  }
}
```

In the above code, we define a custom scroll physics class `CustomScrollPhysics` that takes the `rangeStart` and `rangeEnd` as parameters. We override the `applyBoundaryConditions` method to limit the draggable item's movement within the specified range. We also override the `createBallisticSimulation` method to use a scroll spring simulation that respects the range limits.

## Step 2: Implement custom scroll physics in Draggable

Once we have our custom scroll physics class, we can use it with the `physics` property of the `Draggable` widget to apply the desired scrolling behavior.

Here's an example of using our custom scroll physics in a `Draggable` widget:

```dart
Draggable(
  // Other properties...
  physics: CustomScrollPhysics(rangeStart: 0, rangeEnd: 100),
  child: // Your draggable widget here,
  feedback: // Your feedback widget here,
)
```

In the above code, we set the `physics` property of the `Draggable` widget to an instance of our `CustomScrollPhysics` class. We pass the `rangeStart` and `rangeEnd` values to define the range within which the draggable item can be scrolled.

## Conclusion

By creating a custom scroll physics subclass and using it with the `Draggable` widget, we can customize the scrolling behavior to achieve the desired effect. In this tutorial, we learned how to create a custom scroll physics class that limits the draggable item's movement within a specific range.

Remember to experiment with different custom scroll physics implementations to achieve your desired scrolling behavior in your Flutter applications.

#flutter #Draggable #scrolling