---
layout: post
title: "Adding animations to ListView item removal in Flutter."
description: " "
date: 2023-09-15
tags: [flutter, animations]
comments: true
share: true
---

When building a Flutter application with a `ListView`, it's often desirable to add animations when removing items from the list. This can provide a more visually appealing and engaging user experience. In this blog post, we will explore how to achieve this by using the `AnimatedList` widget in Flutter.

## Setting Up the AnimatedList

To begin, we need to set up the `AnimatedList` widget. This widget is similar to the regular `ListView`, but it provides built-in support for animations during item insertion, removal, and reordering.

First, import the necessary libraries:

```dart
import 'package:flutter/material.dart';
```

Next, create a stateful widget that holds the state of the `AnimatedList`:

```dart
class AnimatedListView extends StatefulWidget {
  @override
  _AnimatedListViewState createState() => _AnimatedListViewState();
}
```

Inside the state class `_AnimatedListViewState`, we define a list of items and a GlobalKey for the `AnimatedList`:

```dart
class _AnimatedListViewState extends State<AnimatedListView> {
  List<String> _items = [];
  final GlobalKey<AnimatedListState> _listKey = GlobalKey<AnimatedListState>();
}
```

## Adding and Removing Items

To add and remove items from the `AnimatedList`, we modify the `_items` list and notify the `AnimatedList` about the change. Let's start by adding items:

```dart
void _addItem() {
  setState(() {
    int newIndex = _items.length;
    _items.add("Item $newIndex");

    _listKey.currentState!.insertItem(newIndex);
  });
}
```

In this example, we add a new item to the `_items` list and use the `insertItem` method of the `AnimatedListState` to animate its insertion at `newIndex`.

Next, let's remove items:

```dart
void _removeItem(int index) {
  setState(() {
    _listKey.currentState!.removeItem(
      index,
      (context, animation) => ListTile(
        title: FadeTransition(
          opacity: animation,
          child: Text(_items[index]),
        ),
      ),
      duration: const Duration(milliseconds: 500),
    );
    _items.removeAt(index);
  });
}
```

In this example, we use the `removeItem` method to animate the removal of an item at `index`. We provide a builder function that defines the widget to display during the removal animation (in this case, a fading `ListTile`).

## Using the AnimatedListView

To use the `AnimatedListView` widget, we need to include it in our app's widget tree. Here's an example:

```dart
void main() {
  runApp(MaterialApp(
    home: Scaffold(
      appBar: AppBar(title: const Text('Animated ListView')),
      body: AnimatedListView(),
    ),
  ));
}
```

With this setup, we can now add and remove items from our `AnimatedList` with smooth animation effects.

## Conclusion

Adding animations to the removal of items in a `ListView` can greatly enhance the user experience of a Flutter application. In this blog post, we learned how to use the `AnimatedList` widget to achieve this effect. By following the steps outlined, you can easily incorporate animations into your Flutter apps and provide a more engaging UI experience for your users.

#flutter #animations