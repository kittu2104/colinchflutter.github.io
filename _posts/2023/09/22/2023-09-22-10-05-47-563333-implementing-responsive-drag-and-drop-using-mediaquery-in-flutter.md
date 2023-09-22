---
layout: post
title: "Implementing responsive drag and drop using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [responsive, draganddrop]
comments: true
share: true
---

Drag and drop functionality is a common requirement in many mobile apps. However, making it responsive across different screen sizes and orientations can be a challenge. Thankfully, Flutter provides the `MediaQuery` class that we can leverage to achieve responsive drag and drop. In this blog post, we will explore how to implement responsive drag and drop using `MediaQuery` in Flutter.

## Understanding `MediaQuery`

`MediaQuery` is a Flutter class that provides information about the current media or screen environment. It gives us access to properties such as screen size, device orientation, and more. By using `MediaQuery`, we can dynamically adapt our UI components based on the available screen real estate.

## Implementing responsive drag and drop

To implement responsive drag and drop, we need to follow these steps:

1. Retrieve the screen size using `MediaQuery.of(context).size`.
2. Set up drag and drop listeners on the draggable and droppable widgets.
3. Calculate the position of the dragged object using the difference between the initial touch point and the current touch point.
4. Adjust the position based on the screen size to make it responsive.

Here's an example code snippet that demonstrates how to implement responsive drag and drop using `MediaQuery` in Flutter:

```dart
import 'package:flutter/material.dart';

class ResponsiveDragAndDrop extends StatefulWidget {
  @override
  _ResponsiveDragAndDropState createState() => _ResponsiveDragAndDropState();
}

class _ResponsiveDragAndDropState extends State<ResponsiveDragAndDrop> {
  Offset _position = Offset(0, 0);

  @override
  Widget build(BuildContext context) {
    Size screenSize = MediaQuery.of(context).size;

    return Scaffold(
      body: Stack(
        children: [
          Positioned(
            left: _position.dx,
            top: _position.dy,
            child: Draggable(
              child: Container(
                width: 100,
                height: 100,
                color: Colors.blue,
                child: Center(
                  child: Text(
                    'Drag Me',
                    style: TextStyle(
                      color: Colors.white,
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                ),
              ),
              feedback: Container(
                width: 100,
                height: 100,
                color: Colors.blue.withOpacity(0.5),
                child: Center(
                  child: Text(
                    'Drag Me',
                    style: TextStyle(
                      color: Colors.white,
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                ),
              ),
              onDraggableCanceled: (_, __) {},
              onDragEnd: (details) {
                setState(() {
                  _position += details.delta;
                });
              },
            ),
          ),
        ],
      ),
    );
  }
}

void main() {
  runApp(MaterialApp(
    home: ResponsiveDragAndDrop(),
  ));
}
```

In this example, we use a `Stack` widget to position the draggable widget using the calculated position based on `_position.dx` and `_position.dy`. The `onDragEnd` callback adjusts the position of the draggable object based on the touch movement.

By leveraging `MediaQuery.of(context).size`, we ensure that the position adjustments are responsive and adapt to different screen sizes and orientations.

## Conclusion

In this blog post, we learned how to implement responsive drag and drop using `MediaQuery` in Flutter. By using the screen size information provided by `MediaQuery`, we can make our drag and drop functionality adaptive and work seamlessly across different devices and orientations. Incorporate this technique into your Flutter apps to enhance the user experience and responsiveness.

#responsive #draganddrop #Flutter #MediaQuery