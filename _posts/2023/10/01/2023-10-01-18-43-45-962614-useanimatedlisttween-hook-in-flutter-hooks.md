---
layout: post
title: "useAnimatedListTween hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: [flutter, hooks, flutteranimation, flutterdev]
comments: true
share: true
---

In Flutter, the `useAnimatedListTween` hook is a powerful tool provided by the [Hooks](https://pub.dev/packages/flutter_hooks) package. The hook allows you to create smooth animations for adding, removing, and updating elements in a list.

## Installation

To use the `useAnimatedListTween` hook, you need to add the `flutter_hooks` package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_hooks: ^0.18.0
```

Then, run `flutter pub get` to fetch the package.

## Usage

To get started with `useAnimatedListTween`, import the required libraries:

```dart
import 'package:flutter_hooks/flutter_hooks.dart';
import 'package:flutter/animation.dart';
import 'package:flutter/material.dart';
```

Next, you can define a widget that uses the hook:

```dart
class AnimatedListWidget extends HookWidget {
  @override
  Widget build(BuildContext context) {
    final animateList = useAnimatedListTween<int>(
      initialItems: [1, 2, 3],
      itemRemovedBuilder: _itemRemovedBuilder,
      itemBuilder: _itemBuilder,
    );

    return Scaffold(
      body: ListView.builder(
        itemCount: animateList.length,
        itemBuilder: (_, index) => animateList[index],
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          final index = animateList.length;
          animateList.insert(index, index + 1);
        },
        child: Icon(Icons.add),
      ),
    );
  }

  AnimatedListRemovedItemBuilder<int> _itemRemovedBuilder(
    int value,
    BuildContext context,
    Animation<double> animation,
  ) {
    return (BuildContext context, Animation<double> animation) {
      return FadeTransition(
        opacity: animation,
        child: ListTile(title: Text('$value')),
      );
    };
  }

  AnimatedListItemBuilder<int> _itemBuilder(
    int value,
    BuildContext context,
    Animation<double> animation,
  ) {
    return (BuildContext context, Animation<double> animation) {
      return SizeTransition(
        sizeFactor: animation,
        child: ListTile(title: Text('$value')),
      );
    };
  }
}
```

In the example above, we create an `AnimatedListWidget` widget that contains a `ListView.builder`. The `useAnimatedListTween` hook manages the list of items. When the floating action button is pressed, a new item is added to the list. The `itemBuilder` and `itemRemovedBuilder` callbacks define how items are animated when added or removed.

## Conclusion

The `useAnimatedListTween` hook in the Flutter Hooks package provides a straightforward way to animate elements in a list with smooth transitions. By utilizing this hook, you can enhance the visual appeal and usability of your Flutter applications.

#flutter #hooks #flutteranimation #flutterdev