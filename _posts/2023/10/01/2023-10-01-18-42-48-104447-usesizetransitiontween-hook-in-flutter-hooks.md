---
layout: post
title: "useSizeTransitionTween hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: [FlutterHooks, SizeTransitionTween]
comments: true
share: true
---

Flutter Hooks is a powerful library that simplifies state management in Flutter applications. It provides a set of useful hooks that can be used to enhance the functionality of Flutter widgets. One such hook is `useSizeTransitionTween`, which allows you to create animated size transitions using a `Tween` in Flutter Hooks.

To get started, you'll need to add the Flutter Hooks dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_hooks: ^0.18.0
```

Next, import the required packages in your Dart file:

```dart
import 'package:flutter_hooks/flutter_hooks.dart';
import 'package:flutter/material.dart';
```

Now, you can use the `useSizeTransitionTween` hook to create animated size transitions. Here's an example of how to use it:

```dart
Widget MyAnimatedWidget() {
  final containerSize = useState(Size.zero);

  final animationController = useAnimationController(duration: Duration(seconds: 1));
  final animation = useSizeTransitionTween(
    controller: animationController,
    initialSize: Size.zero,
    endSize: containerSize.value,
  );

  useEffect(() {
    animationController.forward();
    return () => animationController.dispose();
  }, []);

  return AnimatedBuilder(
    animation: animationController,
    builder: (context, child) {
      return Container(
        width: animation.value.width,
        height: animation.value.height,
        color: Colors.blue,
        child: child,
      );
    },
    child: Text("Hello, World!"),
  );
}
```

In the example above, we're using the `useState` hook to maintain the size of a container. We then create an animation controller using the `useAnimationController` hook and pass it to the `useSizeTransitionTween` hook along with the initial and end sizes of the container.

The `useEffect` hook is used to start the animation when the widget is first rendered and clean up the animation controller when the widget is disposed.

Finally, we use the `AnimatedBuilder` widget to build the animated container, using the value from the `useSizeTransitionTween` hook to animate the width and height of the container. The `Text` widget is used as the child of the container for demonstration purposes.

Remember to add appropriate hooks dependencies and widgets according to your project's needs.

Happy coding and enjoy using the `useSizeTransitionTween` hook in Flutter Hooks!

#FlutterHooks #SizeTransitionTween