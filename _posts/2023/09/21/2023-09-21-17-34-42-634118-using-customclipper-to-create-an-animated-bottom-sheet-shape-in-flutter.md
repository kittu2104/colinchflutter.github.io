---
layout: post
title: "Using CustomClipper to create an animated bottom sheet shape in Flutter"
description: " "
date: 2023-09-21
tags: [CustomClipper]
comments: true
share: true
---

In this tutorial, we will learn how to use the `CustomClipper` class in Flutter to create an animated bottom sheet shape. We will be able to customize the shape of the bottom sheet according to our requirements.

## Requirements

Before starting, make sure you have the following installed:

- Flutter SDK
- Dart SDK
- Latest version of Flutter

## Steps

### Step 1: Create a new Flutter project

Start by creating a new Flutter project using the following command:

```dart
flutter create animated_bottom_sheet
cd animated_bottom_sheet
```

### Step 2: Modify the `main.dart` file

Open the `lib/main.dart` file and replace the default code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Animated Bottom Sheet',
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
        title: Text('Animated Bottom Sheet'),
      ),
      body: Center(
        child: RaisedButton(
          onPressed: () {
            showModalBottomSheet(
                context: context, builder: (BuildContext context) => CustomBottomSheet());
          },
          child: Text('Open Bottom Sheet'),
        ),
      ),
    );
  }
}

class CustomBottomSheet extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      height: 200,
      decoration: ShapeDecoration(
        shape: _CustomClipper(),
        color: Colors.white,
      ),
      child: Center(
        child: Text(
          'This is a custom bottom sheet!',
          style: TextStyle(fontSize: 20),
        ),
      ),
    );
  }
}

class _CustomClipper extends CustomClipper<Path> {
  @override
  Path getClip(Size size) {
    Path path = Path();
    path.moveTo(0, 40);
    path.lineTo(0, size.height);
    path.lineTo(size.width, size.height);
    path.lineTo(size.width, 40);
    path.quadraticBezierTo(size.width / 2, 0, 0, 40);
    return path;
  }

  @override
  bool shouldReclip(CustomClipper<Path> oldClipper) {
    return true;
  }
}

```

### Step 3: Run the app

Save the `main.dart` file and run the app using the following command:

```dart
flutter run
```

Once the app is running, click on the "Open Bottom Sheet" button to see the animated bottom sheet with a custom shape.

## Conclusion

In this tutorial, you learned how to use `CustomClipper` in Flutter to create an animated bottom sheet shape. You can now customize the shape of the bottom sheet to fit your app's design requirements. Experiment with different shapes and designs to create a unique user experience.

#Flutter #CustomClipper