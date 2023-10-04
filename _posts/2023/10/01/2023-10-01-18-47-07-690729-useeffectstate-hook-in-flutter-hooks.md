---
layout: post
title: "useEffectState hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: [flutterhooks]
comments: true
share: true
---

Flutter Hooks is a powerful package that provides a way to use hooks in Flutter functional widgets. One of the most commonly used hooks is the `useEffectState` hook, which allows you to manage the state of a widget and perform side effects when the state changes. In this blog post, we will explore how to use the `useEffectState` hook in Flutter Hooks.

## Introduction to useEffectState

The `useEffectState` hook is similar to Flutter's `StatefulWidget` and `State` combination. It creates a stateful value that can be mutated and triggers side effects whenever the state changes. This hook is particularly useful when you need to perform some operations whenever the state of a widget changes, such as making network requests or updating the UI.

## Installation and Usage

Before you can use the `useEffectState` hook, you need to add the `flutter_hooks` package to your pubspec.yaml file:

```dart
dependencies:
  flutter_hooks: ^0.16.0
```

Once you have added the package, you can use the `useEffectState` hook in your functional widgets. Here's an example of how to use it:

```dart
import 'package:flutter_hooks/flutter_hooks.dart';

void main() {
  runApp(MyApp());
}

// Functional widget using useEffectState
class MyApp extends HookWidget {
  @override
  Widget build(BuildContext context) {
    final count = useEffectState<int>(initialData: 0);

    useEffect(() {
      print('Count changed: $count');
    }, [count.value]);

    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Flutter Hooks - useEffectState'),
        ),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: <Widget>[
              Text(
                'Count: ${count.value}',
              ),
              RaisedButton(
                onPressed: () {
                  // Update the count value
                  count.value = count.value + 1;
                },
                child: Text('Increment'),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

In the example above, we create a functional widget `MyApp` that uses the `useEffectState` hook to manage the `count` state. We then use the `useEffect` hook to print a message whenever the `count` value changes. The widget displays the current count value and has a button that increments the count when pressed.

## Conclusion

The `useEffectState` hook in Flutter Hooks is a powerful tool that allows you to easily manage state and perform side effects in functional widgets. It simplifies the process of managing state and makes your code more concise and readable. Give it a try in your Flutter projects and see how it can improve your development experience.

#flutter #flutterhooks