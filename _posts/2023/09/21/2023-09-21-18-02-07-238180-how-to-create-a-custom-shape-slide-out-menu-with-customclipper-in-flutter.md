---
layout: post
title: "How to create a custom shape slide out menu with CustomClipper in Flutter"
description: " "
date: 2023-09-21
tags: [Flutter, SlideOutMenu]
comments: true
share: true
---

In this tutorial, we will learn how to create a custom shape slide out menu using `CustomClipper` in Flutter. The `CustomClipper` class in Flutter allows us to define custom clipping behavior for a widget.

## Prerequisites

Before we start, make sure you have Flutter installed on your machine. You can follow the official Flutter installation guide: [https://flutter.dev/docs/get-started/install](https://flutter.dev/docs/get-started/install)

## Step 1: Set up a new Flutter project

Create a new Flutter project by running the following command in your terminal:

```bash
flutter create custom_shape_menu
```

Change to the project directory:

```bash
cd custom_shape_menu
```

## Step 2: Define a CustomClipper class

Inside the `lib` directory, create a new file called `menu_clipper.dart`. In this file, define a custom clipper class that extends the `CustomClipper` class:

```dart
import 'package:flutter/material.dart';

class MenuClipper extends CustomClipper<Path> {
  @override
  Path getClip(Size size) {
    final path = Path();
    path.moveTo(0, 0);
    path.lineTo(size.width * 0.6, 0);
    path.quadraticBezierTo(
        size.width * 0.63, size.height * 0.03, size.width * 0.65, size.height * 0.1);
    path.lineTo(size.width * 0.8, size.height * 0.8);
    path.quadraticBezierTo(
        size.width * 0.82, size.height * 0.88, size.width, size.height);
    path.lineTo(0, size.height);
    path.close();
    return path;
  }

  @override
  bool shouldReclip(covariant CustomClipper<Path> oldClipper) => false;
}
```

In the `getClip` method, we define the shape of the clipper using a series of lines and quadratic Bezier curves. Adjust the control points to customize the shape according to your preference.

## Step 3: Create a Slide Out Menu

Open the `lib/main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';
import 'package:custom_shape_menu/menu_clipper.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Custom Shape Menu',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Custom Shape Menu'),
      ),
      body: Stack(
        children: [
          ClipPath(
            clipper: MenuClipper(),
            child: Container(
              color: Colors.blue,
              width: double.infinity,
              height: double.infinity,
            ),
          ),
          Center(
            child: Text(
              'Hello, World!',
              style: TextStyle(fontSize: 24, color: Colors.white),
            ),
          ),
        ],
      ),
    );
  }
}
```

In the `MyHomePage` widget, we use the `ClipPath` widget and provide our custom clipper class `MenuClipper` to achieve the desired shape. We then place a `Container` widget inside `ClipPath` to fill the clipped shape with our desired color. In this example, we use blue as the background color.

The `Center` widget contains the text "Hello, World!" which is displayed on top of the slide-out menu.

## Conclusion

In this tutorial, we have learned how to create a custom shape slide out menu using `CustomClipper` in Flutter. Experiment with different control points and shapes to create unique and visually appealing slide out menus for your Flutter app.

If you have any questions or suggestions, feel free to leave a comment below.

#Flutter #SlideOutMenu