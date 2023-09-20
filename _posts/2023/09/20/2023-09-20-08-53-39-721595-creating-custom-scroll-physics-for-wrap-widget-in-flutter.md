---
layout: post
title: "Creating custom scroll physics for Wrap widget in Flutter"
description: " "
date: 2023-09-20
tags: []
comments: true
share: true
---

Scroll physics in Flutter determine the behavior and characteristics of how a scrollable widget responds to user input and animation. While Flutter provides a set of default scroll physics, sometimes you may need to create custom scroll physics to achieve a specific scrolling behavior. In this tutorial, we will explore how to create custom scroll physics for a `Wrap` widget in Flutter.

## Understanding the Problem

By default, the `Wrap` widget in Flutter does not support scrolling. It lays out its children in a wrapping manner based on the available space. However, if you want to enable scrolling for a `Wrap` widget when the children exceed the available space, you need to create custom scroll physics.

## Steps to Create Custom Scroll Physics for Wrap Widget

### Step 1: Extend `ScrollPhysics` Class

First, we need to create a custom class that extends the `ScrollPhysics` class. This allows us to customize the physics of the scrolling behavior. Here's an example of how to create a custom scroll physics class:

```dart
class CustomWrapScrollPhysics extends ScrollPhysics {
  
  const CustomWrapScrollPhysics({ScrollPhysics? parent}) : super(parent: parent);

  @override
  CustomWrapScrollPhysics applyTo(ScrollPhysics? ancestor) {
    return CustomWrapScrollPhysics(parent: buildParent(ancestor));
  }

  @override
  bool shouldAcceptUserOffset(ScrollMetrics position) {
    // Determine whether scrolling should be accepted based on scroll position
    return true; // Replace with your own condition
  }

  @override
  double applyPhysicsToUserOffset(ScrollMetrics position, double offset) {
    // Apply custom physics to the scroll offset
    return offset; // Replace with your custom logic
  }
  
  // Override other scroll physics methods as needed

}
```

### Step 2: Apply Custom Scroll Physics to `ScrollConfiguration`

Next, we need to apply the custom scroll physics to the `Wrap` widget using the `ScrollConfiguration` widget. This allows us to wrap our `Wrap` widget with the custom scroll physics.

```dart
ScrollConfiguration(
  behavior: ScrollBehavior().copyWith(phy