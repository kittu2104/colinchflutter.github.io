---
layout: post
title: "Flutter undo/redo state management"
description: " "
date: 2023-10-10
tags: [stateManagement]
comments: true
share: true
---

Undo and redo functionality is a crucial feature in many applications, allowing users to revert changes and reapply them. In Flutter, implementing undo/redo state management can be achieved with a combination of a state management solution and a data structure to store the state history.

In this blog post, we will explore how to implement undo/redo functionality using the Provider package for state management and a stack data structure to store and manage the state history.

## Table of Contents
- [Setting up the Provider package](#setting-up-the-provider-package)
- [Implementing the state management](#implementing-the-state-management)
- [Creating the undo/redo functionality](#creating-the-undo-redo-functionality)
- [Testing the undo/redo functionality](#testing-the-undo-redo-functionality)
- [Conclusion](#conclusion)

Let's get started!

## Setting up the Provider package
Before we dive into implementing the undo/redo functionality, we need to set up the Provider package for state management.

First, add the `provider` dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  provider: ^4.3.2
```

Then, run `flutter pub get` to fetch the package.

## Implementing the state management
To manage the application state, we can create a simple model class that represents the data we want to track and manage the history for. For example, let's create a `Counter` class with a single property representing the current count:

```dart
class Counter {
  int count;

  Counter(this.count);
}
```

Next, we can create a state management class that extends `ChangeNotifier` provided by the Provider package. This class will store and handle the state history. We'll call it `CounterState`:

```dart
class CounterState extends ChangeNotifier {
  Stack<Counter> _stateHistory = Stack<Counter>();
  int _currentStateIndex = -1;

  void increment() {
    _stateHistory.push(Counter(_stateHistory.isEmpty ? 1 : _stateHistory.top().count + 1));
    _currentStateIndex++;
    notifyListeners();
  }

  void undo() {
    if (_currentStateIndex > 0) {
      _currentStateIndex--;
      notifyListeners();
    }
  }

  void redo() {
    if (_currentStateIndex < _stateHistory.length - 1) {
      _currentStateIndex++;
      notifyListeners();
    }
  }

  Counter getCurrentState() {
    if (_currentStateIndex >= 0 && _currentStateIndex < _stateHistory.length) {
      return _stateHistory[_currentStateIndex];
    }
    return null;
  }
}
```

In the `CounterState` class, we use a stack data structure to store instances of the `Counter` class. Each time the count is incremented, a new `Counter` object is added to the stack. The `currentStateIndex` keeps track of the current state position in the stack.

The `notifyListeners()` method is called whenever the state changes, which updates any widgets that are listening to this state.

## Creating the undo/redo functionality
To implement the undo/redo functionality, we need to provide methods to undo and redo the state changes in the `CounterState` class.

The `undo()` method decrements the `_currentStateIndex` by one if it's greater than 0 and calls `notifyListeners()`. This moves the state to the previous state in the stack.

The `redo()` method increments the `_currentStateIndex` by one if it's less than the length of the state history and calls `notifyListeners()`. This moves the state to the next state in the stack.

## Testing the undo/redo functionality
To test the undo/redo functionality, we can create a simple Flutter application that uses the `CounterState` class we implemented. Here's an example `main.dart` file:

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ChangeNotifierProvider(
      create: (_) => CounterState(),
      child: MaterialApp(
        title: 'Undo/Redo Demo',
        theme: ThemeData(primarySwatch: Colors.blue),
        home: MyHomePage(),
      ),
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    CounterState counterState = Provider.of<CounterState>(context, listen: true);
    Counter currentState = counterState.getCurrentState();

    return Scaffold(
      appBar: AppBar(
        title: Text('Undo/Redo Demo'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text(
              'Count: ${currentState?.count ?? 0}',
              style: TextStyle(fontSize: 20),
            ),
            SizedBox(height: 16),
            RaisedButton(
              onPressed: () {
                counterState.increment();
              },
              child: Text('Increment'),
            ),
            RaisedButton(
              onPressed: () {
                counterState.undo();
              },
              child: Text('Undo'),
            ),
            RaisedButton(
              onPressed: () {
                counterState.redo();
              },
              child: Text('Redo'),
            ),
          ],
        ),
      ),
    );
  }
}
```

In this example, we use the `Provider` widget to provide the `CounterState` to the widget tree. The `MyHomePage` widget listens to the `CounterState` and displays the current count. The increment, undo, and redo buttons call the respective methods of `CounterState` to modify the state.

## Conclusion
Undo/redo functionality is a useful feature in many applications. By utilizing the Provider package for state management and a stack data structure to store the state history, we can easily implement undo/redo in our Flutter applications.

By following the steps outlined in this blog post, you now have a solid foundation to implement undo/redo state management in your own Flutter projects.

Happy coding! 🚀

#flutter #stateManagement