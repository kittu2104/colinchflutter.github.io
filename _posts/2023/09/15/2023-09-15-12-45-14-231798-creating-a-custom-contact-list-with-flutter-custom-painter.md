---
layout: post
title: "Creating a custom contact list with Flutter Custom Painter"
description: " "
date: 2023-09-15
tags: [custompainter]
comments: true
share: true
---

Flutter Custom Painter is a powerful tool that allows you to create custom UI components in Flutter by painting on a canvas. In this tutorial, we will explore how to create a custom contact list by leveraging the capabilities of Flutter Custom Painter.

## Prerequisites

Before we begin, make sure you have Flutter and Dart installed on your machine. You should also have a basic understanding of how Flutter widgets and layouts work.

## Getting Started

To get started, create a new Flutter project and open it in your preferred code editor. Inside the project, create a new Dart file called `custom_contact_list.dart` to write our custom contact list component.

## Setting up the Custom Painter

First, import the necessary libraries:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/rendering.dart';
```

Next, create a new class that extends `CustomPainter`:

```dart
class CustomContactListPainter extends CustomPainter {
  // Implement necessary methods here
}
```

## Implementing the `CustomPainter` Methods

Inside the `CustomContactListPainter` class, we need to implement the `paint` and `shouldRepaint` methods. The `paint` method is where we actually draw the contact list, and the `shouldRepaint` method determines whether the `CustomPainter` needs to repaint itself.

```dart
class CustomContactListPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // Implement your code to draw the contact list here
  }

  @override
  bool shouldRepaint(CustomContactListPainter oldDelegate) {
    // Determine whether the CustomPainter needs to repaint
    return false;
  }
}
```

## Drawing the Contact List

To draw the contact list, we need to utilize the `paint` method. Let's start by drawing a basic background for our component:

```dart
@override
void paint(Canvas canvas, Size size) {
  final backgroundPaint = Paint()
    ..color = Colors.white
    ..style = PaintingStyle.fill;
  
  canvas.drawRect(
    Rect.fromLTWH(0, 0, size.width, size.height),
    backgroundPaint,
  );
}
```

Next, let's draw the individual contact items. For simplicity, we'll just draw a rectangle for each contact:

```dart
@override
void paint(Canvas canvas, Size size) {
  // Draw the background
  
  // Draw individual contact items
  final contactItemPaint = Paint()
    ..color = Colors.grey
    ..style = PaintingStyle.fill;
  
  final contactItemWidth = size.width;
  final contactItemHeight = 60.0;
  
  for (int i = 0; i < 10; i++) {
    final itemRect = Rect.fromLTWH(
      0,
      i * contactItemHeight,
      contactItemWidth,
      contactItemHeight,
    );
    
    canvas.drawRect(itemRect, contactItemPaint);
  }
}
```

## Applying the Custom Painter

To use the custom contact list painter in your Flutter app, add a `CustomPaint` widget to your app's widget tree and provide an instance of the `CustomContactListPainter` class as its `painter` property:

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: Text('Custom Contact List'),
    ),
    body: CustomPaint(
      painter: CustomContactListPainter(),
    ),
  );
}
```

## Conclusion

In this tutorial, we learned how to create a custom contact list using Flutter Custom Painter. We explored the basic setup, implemented the necessary `CustomPainter` methods, and drew the contact list items using the canvas. With this knowledge, you can now extend the functionality and customize the appearance of your contact list further.

#flutter #custompainter