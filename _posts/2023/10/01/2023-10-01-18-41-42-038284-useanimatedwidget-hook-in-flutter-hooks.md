---
layout: post
title: "useAnimatedWidget hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: [animation]
comments: true
share: true
---

Flutter Hooks is a powerful library that provides a set of pre-built hooks to simplify state management in Flutter applications. One such useful hook is `useAnimatedWidget`, which allows you to easily create animated widgets with the help of the AnimationController.

## Getting Started

Before diving into the use of `useAnimatedWidget`, make sure you have Flutter Hooks added to your project by following the installation guide [here](https://pub.dev/packages/flutter_hooks).

Once you have Flutter Hooks installed, you can start using the `useAnimatedWidget` hook.

## Understanding useAnimatedWidget

The `useAnimatedWidget` hook is a specialized hook that helps in creating animated widgets. It takes an animated builder function as a parameter, which is responsible for building the animated widget. This builder function receives an Animation object that can be used to drive the animation.

Here's an example of how to use the `useAnimatedWidget` hook:

```dart
import 'package:flutter_hooks/flutter_hooks.dart';

class MyApp extends HookWidget {
  @override
  Widget build(BuildContext context) {
    final animationController = useAnimationController();
    final animation = useAnimation(animationController);

    return Scaffold(
      body: Center(
        child: useAnimatedWidget(
          animation: animation,
          builder: (context, animation) {
            return Container(
              width: animation * 200,
              height: animation * 200,
              color: Colors.blue,
            );
          },
        ),
      ),
    );
  }
}
```

In the above example, we create an `animationController` using the `useAnimationController` hook. We then fetch the animation state using the `useAnimation` hook. Finally, we wrap our custom animated widget inside the `useAnimatedWidget` hook, passing our animation object and builder function as parameters.

## Conclusion

The `useAnimatedWidget` hook in Flutter Hooks makes it easy to create animated widgets by leveraging the power of the AnimationController. It simplifies the process of managing animation state and allows for more concise and readable code.

Using `useAnimatedWidget` can greatly enhance the interactivity and user experience of your Flutter applications. So give it a try and see how it can improve your app's animations.

#flutter #animation