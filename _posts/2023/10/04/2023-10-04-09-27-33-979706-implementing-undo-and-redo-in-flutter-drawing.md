---
layout: post
title: "Implementing undo and redo in Flutter drawing"
description: " "
date: 2023-10-04
tags: [drawing, creating]
comments: true
share: true
---

When building a drawing app in Flutter, it's often necessary to provide an undo and redo functionality for users. This allows them to easily revert their drawing actions or redo them if needed. In this tutorial, we will explore how to implement undo and redo functionality in a Flutter drawing app.

## Table of Contents
- [Drawing App Setup](#drawing-app-setup)
- [Creating an Undo Stack](#creating-an-undo-stack)
- [Implementing Undo Functionality](#implementing-undo-functionality)
- [Implementing Redo Functionality](#implementing-redo-functionality)
- [Conclusion](#conclusion)

## Drawing App Setup

Assuming you already have a basic drawing app setup in Flutter, we will start by adding the necessary variables and imports needed for implementing undo and redo functionality.

```dart
import 'package:flutter/material.dart';

class DrawingApp extends StatefulWidget {
  @override
  _DrawingAppState createState() => _DrawingAppState();
}

class _DrawingAppState extends State<DrawingApp> {
  List<CustomPath> _paths = [];
  List<CustomPath>? _undoPaths;
  
  // Rest of your drawing app code...
}
```

Here, we have created a `_paths` list to store the drawn paths and `_undoPaths` list to keep track of the paths that can be undone.

## Creating an Undo Stack

Before we can implement undo and redo functionality, we need to create a stack to hold the paths that can be undone. We will use the `dart:collection` package for this purpose.

```dart
import 'package:flutter/foundation.dart';

class _DrawingAppState extends State<DrawingApp> {
  // ...

  // Create an UndoRedoStack using a LinkedList
  UndoRedoStack<CustomPath> _undoRedoStack = UndoRedoStack();
  
  // ...

  @override
  Widget build(BuildContext context) {
    // ...
  }
}

class UndoRedoStack<T> {
  LinkedList<T> _list = LinkedList<T>();

  void push(T value) {
    _list.addLast(value);
  }

  T? pop() {
    if (_list.isEmpty) return null;
    final last = _list.last;
    _list.removeLast();
    return last;
  }
}
```

Here, we have defined the `UndoRedoStack` class using a `LinkedList`, which provides efficient push and pop operations. We have also created an `_undoRedoStack` instance in our `_DrawingAppState` class.

## Implementing Undo Functionality

To enable undo functionality, we need to add a method that will pop the last drawn path from the `_paths` list and push it to the `_undoRedoStack`. This can be done whenever the user triggers an undo action.

```dart
class _DrawingAppState extends State<DrawingApp> {
  // ...

  void _undo() {
    setState(() {
      final lastPath = _paths.isNotEmpty ? _paths.removeLast() : null;
      if (lastPath != null) {
        _undoRedoStack.push(lastPath);
      }
    });
  }

  @override
  Widget build(BuildContext context) {
    // ...
  }
}
```

In the defined `_undo` method, we remove the last path from `_paths` if it's not empty, and then push that path to the `_undoRedoStack`.

## Implementing Redo Functionality

Similarly, we can add a method to implement redo functionality. This method will pop the last path from `_undoRedoStack` and add it back to the `_paths` list.

```dart
class _DrawingAppState extends State<DrawingApp> {
  // ...

  void _redo() {
    setState(() {
      final lastPath = _undoRedoStack.pop();
      if (lastPath != null) {
        _paths.add(lastPath);
      }
    });
  }

  @override
  Widget build(BuildContext context) {
    // ...
  }
}
```

In the `_redo` method, we pop the last path from `_undoRedoStack` and add it back to `_paths` if it exists.

## Conclusion

In this tutorial, we have learned how to implement undo and redo functionality in a Flutter drawing app. By creating an undo stack using a linked list and implementing the undo and redo methods, users can easily revert or redo their drawing actions. Incorporating undo and redo functionality can enhance the user experience and provide greater flexibility when working with a drawing app in Flutter.