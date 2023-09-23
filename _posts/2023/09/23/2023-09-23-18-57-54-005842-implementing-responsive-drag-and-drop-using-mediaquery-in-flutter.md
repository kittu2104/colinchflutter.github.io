---
layout: post
title: "Implementing responsive drag and drop using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [flutter, responsivedesign]
comments: true
share: true
---

Drag and drop functionality is a commonly used feature in many mobile applications. It allows users to move elements around the screen effortlessly. In this blog post, we will explore how to implement a responsive drag and drop feature using `MediaQuery` in Flutter.

## Understanding MediaQuery

`MediaQuery` is a class in Flutter that provides information about the current device's size and orientation. It gives developers the ability to create responsive designs that adapt to different screen sizes.

## Setting up the project

To get started, create a new Flutter project and add the necessary dependencies in the `pubspec.yaml` file.

```dart
dependencies:
  flutter:
    sdk: flutter
  flutter_multi_drag:
```

Run `flutter pub get` to fetch the dependencies.

## Implementing drag and drop

1. Start by importing the necessary packages.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_multi_drag/flutter_multi_drag.dart';
```

2. Create a `Draggable` widget that represents the element that can be dragged.

```dart
class DraggableItem extends StatefulWidget {
  @override
  _DraggableItemState createState() => _DraggableItemState();
}

class _DraggableItemState extends State<DraggableItem> {
  Offset position = Offset(0, 0);

  @override
  Widget build(BuildContext context) {
    return Positioned(
      left: position.dx,
      top: position.dy,
      child: Draggable(
        child: Container(
          width: 100,
          height: 100,
          color: Colors.blue,
        ),
        feedback: Container(
          width: 100,
          height: 100,
          color: Colors.blue.withOpacity(0.5),
        ),
        onDraggableCanceled: (velocity, offset) {
          setState(() {
            position = offset;
          });
        },
      ),
    );
  }
}
```

3. Create a `DragTarget` widget that represents the area where the draggable elements can be dropped.

```dart
class DropTarget extends StatefulWidget {
  @override
  _DropTargetState createState() => _DropTargetState();
}

class _DropTargetState extends State<DropTarget> {
  List<Offset> positions = [];

  @override
  Widget build(BuildContext context) {
    return Stack(
      children: [
        for (var position in positions)
          Positioned(
            left: position.dx,
            top: position.dy,
            child: Container(
              width: 100,
              height: 100,
              color: Colors.red,
            ),
          ),
        DragTarget(
          builder: (context, candidateData, rejectedData) {
            return Container(
              width: MediaQuery.of(context).size.width,
              height: MediaQuery.of(context).size.height,
            );
          },
          onAccept: (data) {
            setState(() {
              positions.add(data);
            });
          },
        ),
      ],
    );
  }
}
```

4. Finally, create a widget that contains both the `DraggableItem` and `DropTarget`.

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: MultiDrag(
        child: Stack(
          children: [
            DraggableItem(),
            DropTarget(),
          ],
        ),
      ),
    );
  }
}
```

## Making it responsive

To make the drag and drop feature responsive, we can utilize the `MediaQuery` class to determine the available screen size and adjust the layout accordingly.

```dart
class _DraggableItemState extends State<DraggableItem> {
  // ...

  double itemSize = 100;

  @override
  Widget build(BuildContext context) {
    final screenWidth = MediaQuery.of(context).size.width;
    final screenHeight = MediaQuery.of(context).size.height;

    return Positioned(
      left: position.dx * screenWidth,
      top: position.dy * screenHeight,
      child: Draggable(
        child: Container(
          width: itemSize,
          height: itemSize,
          color: Colors.blue,
        ),
        // ...
      ),
    );
  }
}
```

By multiplying the `position` values with the screen dimensions, we can ensure that the draggable element will be positioned proportionally on different device screens.

## Conclusion

Implementing a responsive drag and drop feature using `MediaQuery` in Flutter is a powerful way to make your app adapt to various screen sizes. By leveraging the `MediaQuery` class and adjusting the layout based on device dimensions, you can create a seamless user experience across different devices.

#flutter #responsivedesign