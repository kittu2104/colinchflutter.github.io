---
layout: post
title: "Drawing text in Flutter Canvas"
description: " "
date: 2023-10-04
tags: [canvas]
comments: true
share: true
---

One of the powerful features of Flutter is its ability to perform custom drawing with the help of the `Canvas` class. With `Canvas`, you can draw shapes, lines, and even text on the screen. In this blog post, we'll explore how to draw text using the `Canvas` class in Flutter.

## Prerequisites

Make sure you have Flutter SDK installed and set up on your machine. You can refer to Flutter's official documentation for installation instructions.

## Creating a Custom Paint Widget

To draw text on the canvas, we first need to create a custom `CustomPaint` widget. This widget will provide a canvas on which we can perform custom drawing operations. Here's an example of how to create a `CustomPaint` widget:

```dart
import 'package:flutter/material.dart';

class MyCustomPaint extends CustomPaint {
  @override
  void paint(Canvas canvas, Size size) {
    // Custom drawing operations
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) {
    return true;
  }
}
```

In the above code snippet, we extend the `CustomPaint` class and override the `paint` method. This is where we'll perform all the custom drawing operations. The `shouldRepaint` method tells Flutter whether the widget should be repainted when its underlying data changes.

## Drawing Text on the Canvas

To draw text on the canvas, we can use the `drawText` method of the `Canvas` class. Here's an example of how to draw text using Flutter's `Canvas` class:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/rendering.dart';

class MyCustomPaint extends CustomPaint {
  @override
  void paint(Canvas canvas, Size size) {
    final textStyle = TextStyle(fontSize: 24, color: Colors.black);
    final textSpan = TextSpan(text: 'Hello, Flutter!', style: textStyle);
    final textPainter = TextPainter(
      text: textSpan,
      textAlign: TextAlign.center,
      textDirection: TextDirection.ltr,
    );
    textPainter.layout(minWidth: 0, maxWidth: size.width);
    final textOffset = Offset(
      (size.width - textPainter.width) / 2,
      (size.height - textPainter.height) / 2,
    );
    textPainter.paint(canvas, textOffset);
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) {
    return true;
  }
}
```

In the code above, we first create a `TextStyle` and a `TextSpan` with the desired text and style. We then create a `TextPainter` and pass in the `textSpan`, `textAlign`, and `textDirection`. We then call `layout` on the `textPainter` to set the constraints for the text layout. Finally, we calculate the `textOffset` and call `paint` on the `textPainter` to draw the text on the canvas.

## Using the Custom Paint Widget

To use the custom paint widget, we need to add it to the widget tree. We can achieve this by adding the `CustomPaint` widget as a child to a `Container`, `Column`, or any other widget that can contain children. Here's an example:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: Center(
          child: Container(
            width: 300,
            height: 300,
            child: MyCustomPaint(),
          ),
        ),
      ),
    );
  }
}
```

In the main method, we create a `MyApp` widget that is a `MaterialApp` with a `Scaffold` as its home. Inside the `Scaffold`, we use a `Center` widget to center the `Container` that contains the `MyCustomPaint` widget.

## Conclusion

Drawing text using the `Canvas` class in Flutter is simple yet powerful. By creating a custom `CustomPaint` widget and using the `TextPainter` class, we can easily add text to our custom drawings. This opens up a world of possibilities for creating rich and interactive UIs in Flutter.

#flutter  #canvas