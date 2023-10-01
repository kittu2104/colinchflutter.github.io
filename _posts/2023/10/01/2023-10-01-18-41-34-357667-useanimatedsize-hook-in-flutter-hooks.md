---
layout: post
title: "useAnimatedSize hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: []
comments: true
share: true
---

Flutter Hooks is a library that provides a set of [React Hooks](https://reactjs.org/docs/hooks-intro.html)-inspired hooks for Flutter. It allows developers to write more concise and reusable code by managing state and side effects in a functional manner. One useful hook provided by Flutter Hooks is `useAnimatedSize`, which allows for easy implementation of animated size changes in your Flutter applications.

In this blog post, we will explore how to use the `useAnimatedSize` hook to create dynamic and animated size transformations in your Flutter widgets.

## Prerequisites

Before we proceed, make sure your Flutter project has Flutter Hooks properly integrated. You can follow the installation instructions on the [Flutter Hooks GitHub](https://github.com/rrousselGit/flutter_hooks) page to add Flutter Hooks as a dependency to your `pubspec.yaml` file.

## Getting Started

To use the `useAnimatedSize` hook, you'll need to import the `useAnimatedSize` function from the Flutter Hooks library. Let's see an example of how to use this hook in a simple Flutter widget:

```dart
import 'package:flutter_hooks/flutter_hooks.dart';

class MyWidget extends HookWidget {
  @override
  Widget build(BuildContext context) {
    final isExpanded = useState(false);

    final expandedSize = useAnimatedSize(
      child: _buildContent(),
      vsync: useSingleTickerProvider(),
      duration: const Duration(milliseconds: 300),
      curve: Curves.easeInOut,
    );

    return GestureDetector(
      onTap: () => isExpanded.value = !isExpanded.value,
      child: Container(
        width: 200,
        height: isExpanded.value ? expandedSize.height : 50,
        color: Colors.blue,
        child: expandedSize.child,
      ),
    );
  }

  Widget _buildContent() {
    // TODO: Implement your widget content
  }
}
```

In the above example, we have a widget called `MyWidget` that uses the `useAnimatedSize` hook. The `isExpanded` variable is a state variable that keeps track of whether the widget is expanded or not.

The `expandedSize` variable is assigned the value of the `useAnimatedSize` hook. It takes in a `child` parameter, which is the content of the widget that will animate its size. Additionally, it requires a `vsync` parameter, which can be obtained using the `useSingleTickerProvider` hook to synchronize with the Flutter engine's timing. You can also specify the `duration` and `curve` parameters to customize the animation.

In the `GestureDetector` widget, we toggle the `isExpanded` value when the user taps on the widget. The height of the `Container` widget is then adjusted based on the value of `isExpanded`, using the `expandedSize` value.

The `_buildContent` method is a placeholder where you can implement the actual content of your widget.

And that's it! You have successfully used the `useAnimatedSize` hook to create dynamic and animated size transformations in your Flutter widget.

## Conclusion

Flutter Hooks provides a powerful set of hooks that make it easier to manage state and side effects in Flutter applications. The `useAnimatedSize` hook, in particular, allows for effortless creation of animated size changes in your widgets.

By implementing dynamic and animated sizing, you can enhance the user experience and add a touch of elegance to your Flutter applications.