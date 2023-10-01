---
layout: post
title: "useDraggable hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: [flutter, flutterhooks]
comments: true
share: true
---

Flutter Hooks is a powerful library that provides various hooks to simplify state management and enhance the development experience in Flutter. One of the useful hooks provided by Flutter Hooks is the `useDraggable` hook, which allows us to implement drag and drop functionality in our Flutter applications effortlessly. In this blog post, we will explore how to use the `useDraggable` hook in Flutter Hooks.

## Installation

Before we start, make sure you have Flutter Hooks added as a dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_hooks: ^0.18.0
```

## Usage

To use the `useDraggable` hook, we first need to import it:

```dart
import 'package:flutter_hooks/flutter_hooks.dart';
```

Next, let's define a widget where we want to implement drag and drop functionality. 

```dart
Widget buildDraggableWidget() {
  return HookBuilder(
    builder: (BuildContext context) {
      final draggableState = useDraggable(Duration(seconds: 1), () {
        // Handle onDragStart
      }, (offset) {
        // Handle onDragUpdate
      }, () {
        // Handle onDragEnd
      });

      return GestureDetector(
        behavior: HitTestBehavior.translucent,
        onPanDown: (details) => draggableState.onDragStart(details.globalPosition),
        onPanUpdate: (details) => draggableState.onDragUpdate(details.globalPosition),
        onPanEnd: (details) => draggableState.onDragEnd(),
        child: Container(
          width: 100,
          height: 100,
          color: draggableState.isDragging ? Colors.blue : Colors.red,
          child: Center(child: Text('Draggable Widget')),
        ),
      );
    },
  );
}
```

In the code above, we wrap our widget inside the `HookBuilder` widget to create a new context for our hook. Then, we call the `useDraggable` hook and pass in the `onDragStart`, `onDragUpdate`, and `onDragEnd` callbacks.

The `useDraggable` hook returns a state object that provides information about the current drag state. We can use the `isDragging` property of the state object to modify the appearance or behavior of our draggable widget.

Inside the `GestureDetector`, we handle the pan events (`onPanDown`, `onPanUpdate`, `onPanEnd`) and call the respective callback functions provided by the `useDraggable` hook.

Finally, we build a container widget as our draggable widget, and we use the `isDragging` property to conditionally change the background color.

## Conclusion

In this blog post, we learned how to use the `useDraggable` hook in Flutter Hooks to implement drag and drop functionality. Flutter Hooks provides an elegant way to handle stateful logic in Flutter applications, and the `useDraggable` hook is just one of the many helpful hooks available. Experiment with different hooks and see how they can simplify your code and enhance your Flutter development experience.

#flutter #flutterhooks