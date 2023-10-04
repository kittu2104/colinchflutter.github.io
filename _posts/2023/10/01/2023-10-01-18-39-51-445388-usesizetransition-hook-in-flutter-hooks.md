---
layout: post
title: "useSizeTransition hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: [FlutterHooks]
comments: true
share: true
---

In Flutter, we often need to animate the size of a widget smoothly and seamlessly. Using the `useSizeTransition` hook from the Flutter Hooks package can simplify this process and make it more efficient.

## What is the `useSizeTransition` Hook?

The `useSizeTransition` hook is a utility provided by the Flutter Hooks package that allows us to animate the size of a widget based on a given animation controller and transition type. It handles the animation logic for us and provides a smooth transition between different widget sizes.

## How to use the `useSizeTransition` Hook

To use the `useSizeTransition` hook, follow these steps:

1. Import the Flutter Hooks package:
```dart
import 'package:flutter_hooks/flutter_hooks.dart';
```

2. Create an animation controller:
```dart
final _animationController = useAnimationController(
  duration: Duration(seconds: 1),
);
```

3. Define a transition type:
```dart
final _transitionType = useEnum(SizeTransitionType.expand);
```

4. Use the `useSizeTransition` hook:
```dart
final _sizeTransition = useSizeTransition(
  controller: _animationController,
  transitionType: _transitionType.value,
  child: YourWidget(),
);
```

5. Start and control the animation:
```dart
_animationController.forward();  // Start the animation
_animationController.reverse();  // Reverse the animation
```

6. Use `_sizeTransition` as your animated widget:
```dart
return Scaffold(
  body: Center(
    child: _sizeTransition,
  ),
);
```

## Available Transition Types

The `useSizeTransition` hook supports the following transition types:

- `SizeTransitionType.expand`: Expands the widget to fill the available space.
- `SizeTransitionType.shrink`: Shrinks the widget to its minimum size.
- `SizeTransitionType.scale`: Animates the widget by scaling it up or down.
- `SizeTransitionType.fade`: Animates the widget by fading it in or out.

## Conclusion

The `useSizeTransition` hook from the Flutter Hooks package is a powerful tool for creating smooth and efficient size animations in Flutter. By following the steps outlined above, you can easily incorporate size transitions into your Flutter applications. 

Make sure to check the [official Flutter Hooks documentation](https://pub.dev/packages/flutter_hooks) for more details and examples.

#flutter #FlutterHooks