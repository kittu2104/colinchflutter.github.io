---
layout: post
title: "How to create a circular or rounded shape using CustomClipper in Flutter"
description: " "
date: 2023-09-21
tags: [customshape]
comments: true
share: true
---

Flutter provides a powerful set of widgets and APIs to perform custom painting. One of these widgets is `CustomClipper`, which allows you to create custom shapes for clipping or masking various child widgets.

In this tutorial, we will learn how to create a circular or rounded shape using `CustomClipper` in Flutter.

## Step 1: Add Dependencies

Before we start, make sure you have the necessary dependencies added in your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
```

## Step 2: Create a CustomClipper

Create a new file called `circle_clipper.dart` and define a new class called `CircleClipper` that extends `CustomClipper<Path>`:

```dart
import 'package:flutter/material.dart';

class CircleClipper extends CustomClipper<Path> {
  @override
  Path getClip(Size size) {
    final path = Path();
    final center = Offset(size.width / 2, size.height / 2);
    final radius = size.width / 2;
    path.addOval(Rect.fromCircle(center: center, radius: radius));
    return path;
  }

  @override
  bool shouldReclip(CustomClipper oldClipper) => false;
}
```

In the `getClip` method, we calculate the center and radius of the circle based on the size of the widget. Then, we add an oval shape with the calculated center and radius to the `path`.

The `shouldReclip` method indicates whether a new instance of the clipper should be created when the shape changes. In our case, the shape is constant, so we return `false`.

## Step 3: Use the CustomClipper in a Widget

Now, let's use the `CircleClipper` in a widget. We'll create a simple example in the `main.dart` file:

```dart
import 'package:flutter/material.dart';

import 'circle_clipper.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Circular Shape using CustomClipper'),
        ),
        body: Center(
          child: ClipPath(
            clipper: CircleClipper(),
            child: Container(
              width: 200,
              height: 200,
              color: Colors.blue,
            ),
          ),
        ),
      ),
    );
  }
}
```

In the `Scaffold` widget, we use the `ClipPath` widget and pass the `CircleClipper` as the `clipper` property. Then, we wrap the `Container` widget inside the `ClipPath` to apply the circular shape to it. Adjust the `width`, `height`, and `color` of the `Container` to suit your needs.

## Step 4: Run the App

Save the files and run the app on your device or emulator. You should see a circular shape with the specified color displayed on the screen.

Congratulations! You successfully created a circular or rounded shape using `CustomClipper` in Flutter.

#flutter #customshape