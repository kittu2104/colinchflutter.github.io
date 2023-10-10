---
layout: post
title: "Flutter ChangeNotifier class"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

In Flutter, the `ChangeNotifier` class plays a crucial role in implementing the state management pattern known as Provider. It is part of the `flutter/foundation.dart` package and is used to notify listeners when there is a change in state. This allows your app to reactively update the UI when the underlying data changes.

## Creating a ChangeNotifier

To create a `ChangeNotifier` class, you need to extend the `ChangeNotifier` class and define the necessary data and methods for managing state.

Here's an example of a simple `Counter` class that extends `ChangeNotifier`:

```dart
import 'package:flutter/foundation.dart';

class Counter with ChangeNotifier {
  int _count = 0;

  int get count => _count;

  void increment() {
    _count++;
    notifyListeners();
  }
}
```

In this example, the `Counter` class has a private property `_count` to store the value of the counter. The `get count` method exposes the current value of the counter to external widgets. The `increment` method increments the counter and uses the `notifyListeners` method to notify all the registered listeners about the change.

## Consuming a ChangeNotifier

To consume a `ChangeNotifier` and listen for changes, you can use the `Provider` package along with the `Consumer` widget. The `Consumer` widget automatically rebuilds the UI whenever the state of the `ChangeNotifier` changes.

Here's an example of how you can use the `Consumer` widget to consume the `Counter` class:

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

class CounterScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Counter')),
      body: Center(
        child: Consumer<Counter>(
          builder: (context, counter, child) {
            return Text('Count: ${counter.count}');
          },
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          Provider.of<Counter>(context, listen: false).increment();
        },
        child: Icon(Icons.add),
      ),
    );
  }
}
```

In this example, the `Consumer` widget listens to changes in the `Counter` class. Inside the `builder` method, you have access to the current state of the `Counter` class. Whenever the `Counter`'s state changes, the `builder` method is called, and the UI is updated accordingly.

## Summary

In Flutter, the `ChangeNotifier` class is an essential part of implementing state management using the Provider pattern. By extending the `ChangeNotifier` class, you can create classes that notify listeners about changes in state. The `Consumer` widget is then used to consume the state and update the UI reactively.