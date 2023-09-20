---
layout: post
title: "How to change scroll velocity with custom scroll physics in Flutter"
description: " "
date: 2023-09-20
tags: [Flutter, FlutterPhysics]
comments: true
share: true
---

In Flutter, scroll physics control the behavior of scrolling, such as the velocity and friction applied to the scroll movement. By default, Flutter provides a set of predefined scroll physics, but you can also create your own custom scroll physics to change the scroll velocity.

## Creating Custom Scroll Physics

To change the scroll velocity, you need to create a custom scroll physics class. Here's an example of how you can achieve this:

```dart
import 'package:flutter/gestures.dart';
import 'package:flutter/widgets.dart';

class CustomScrollPhysics extends ScrollPhysics {
  final double velocityMultiplier;

  CustomScrollPhysics({this.velocityMultiplier}) : super();

  @override
  CustomScrollPhysics applyTo(ScrollPhysics ancestor) {
    return CustomScrollPhysics(velocityMultiplier: velocityMultiplier) 
          ..init(ancestor);
  }

  @override
  Simulation createBallisticSimulation(
      ScrollMetrics position, double velocity) {
    final double adjustedVelocity = velocity * velocityMultiplier;
    return super.createBallisticSimulation(position, adjustedVelocity);
  }
}
```

In the above code, we create a new class called `CustomScrollPhysics` by extending the `ScrollPhysics` class. We add a custom property `velocityMultiplier` to adjust the scrolling velocity.

The `applyTo` method is used to create a new instance of the custom scroll physics and copy the necessary configurations from the ancestor physics.

The `createBallisticSimulation` method is overridden to adjust the scrolling velocity by multiplying it with the `velocityMultiplier`.

## Applying Custom Scroll Physics

Once you have created the custom scroll physics, you can apply it to a `ListView`, `ScrollView`, or any widget that scrolls. Here's an example of how to apply the custom scroll physics to a `ListView`:

```dart
ListView.builder(
  physics: CustomScrollPhysics(velocityMultiplier: 2.0),
  itemCount: 100,
  itemBuilder: (context, index) {
    return ListTile(title: Text('Item $index'));
  },
);
```

In the above code, we set the `physics` property of the `ListView.builder` to an instance of our `CustomScrollPhysics` class with a `velocityMultiplier` of `2.0`. This will increase the scroll velocity by two times compared to the default scroll physics.

## Conclusion

Custom scroll physics in Flutter allows you to change the scroll velocity and customize the scrolling behavior based on your requirements. By creating a custom scroll physics class and applying it to the scrollable widgets, you can have fine-grained control over how your app handles scrolling.

#Flutter #FlutterPhysics