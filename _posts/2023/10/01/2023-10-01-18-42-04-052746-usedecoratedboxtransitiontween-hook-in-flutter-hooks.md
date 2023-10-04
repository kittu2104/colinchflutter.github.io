---
layout: post
title: "useDecoratedBoxTransitionTween hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: [Hooks]
comments: true
share: true
---

Flutter Hooks is a powerful library that enhances the functionality and reusability of Flutter applications. One of the useful hooks provided by Flutter Hooks is `useDecoratedBoxTransitionTween`. In this blog post, we will dive into the details of this hook and explore how it can be used effectively in Flutter development.

## What is `useDecoratedBoxTransitionTween`?

`useDecoratedBoxTransitionTween` is a hook that allows you to create a transition animation between two `BoxDecoration` objects. It takes in the `beginDecoration` and `endDecoration` as input and returns the intermediate decoration values during the animation.

## Usage Example

Here's an example that demonstrates how to use `useDecoratedBoxTransitionTween` hook to create a transition animation:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_hooks/flutter_hooks.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends HookWidget {
  @override
  Widget build(BuildContext context) {
    final DecorationTween decorationTween = useDecoratedBoxTransitionTween(
      beginDecoration: BoxDecoration(
        color: Colors.blue,
        borderRadius: BorderRadius.circular(10.0),
      ),
      endDecoration: BoxDecoration(
        color: Colors.red,
        borderRadius: BorderRadius.circular(30.0),
      ),
    );

    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Decorated Box Transition Tween'),
        ),
        body: Center(
          child: AnimatedBuilder(
            animation: decorationTween,
            builder: (BuildContext context, Widget child) {
              return DecoratedBox(
                decoration: decorationTween.evaluate(
                  AlwaysStoppedAnimation(0.5),
                ),
                child: SizedBox(
                  width: 200,
                  height: 200,
                ),
              );
            },
          ),
        ),
      ),
    );
  }
}
```

In the above example, we create a `DecorationTween` using `useDecoratedBoxTransitionTween` and specify the `beginDecoration` and `endDecoration`. We use this tween in the `AnimatedBuilder` widget to animate the `DecoratedBox` widget. The animation is controlled by passing an `AlwaysStoppedAnimation` with a value between 0.0 and 1.0 to the `decorationTween.evaluate` method.

## Conclusion

The `useDecoratedBoxTransitionTween` hook provided by Flutter Hooks simplifies the process of creating transition animations between `BoxDecoration` objects. By using this hook, you can easily add visually appealing animations to your Flutter app. It's essential to explore other hooks provided by Flutter Hooks to enhance your Flutter development experience.

#Flutter #Hooks