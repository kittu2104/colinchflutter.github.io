---
layout: post
title: "How to create a custom shape button group with CustomClipper in Flutter"
description: " "
date: 2023-09-21
tags: [flutter, customshape, button, flutterdevelopment]
comments: true
share: true
---

Flutter provides a powerful CustomPaint widget that allows you to create custom shapes and graphics. In this tutorial, we will learn how to utilize the CustomClipper class to create a custom shape button group in Flutter.

## Step 1: Setting up the project

First, let's create a new Flutter project by running the following command in your terminal:

```dart
flutter create custom_shape_button_group
```

## Step 2: Implementing the CustomClipper class

Next, open the `lib/main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';

class ButtonGroupClipper extends CustomClipper<Path> {
  @override
  Path getClip(Size size) {
    final path = Path();
    path.moveTo(size.width * 0.5, size.height);
    path.lineTo(size.width * 0.8, size.height);
    path.arcToPoint(
      Offset(size.width, size.height * 0.5),
      radius: Radius.circular(size.height * 0.4),
    );
    path.arcToPoint(
      Offset(size.width * 0.8, 0),
      radius: Radius.circular(size.height * 0.4),
    );
    path.lineTo(size.width * 0.5, 0);
    path.close();
    return path;
  }

  @override
  bool shouldReclip(covariant CustomClipper<Path> oldClipper) => false;
}

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Custom Shape Button Group'),
      ),
      body: Center(
        child: ClipPath(
          clipper: ButtonGroupClipper(),
          child: Container(
            width: 200,
            height: 64,
            color: Colors.blue,
            child: Row(
              mainAxisAlignment: MainAxisAlignment.spaceEvenly,
              children: [
                FlatButton(
                  onPressed: () {},
                  child: Text(
                    'Button 1',
                    style: TextStyle(color: Colors.white),
                  ),
                ),
                FlatButton(
                  onPressed: () {},
                  child: Text(
                    'Button 2',
                    style: TextStyle(color: Colors.white),
                  ),
                ),
                FlatButton(
                  onPressed: () {},
                  child: Text(
                    'Button 3',
                    style: TextStyle(color: Colors.white),
                  ),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}

void main() {
  runApp(MaterialApp(
    home: HomePage(),
  ));
}
```

## Step 3: Running the app

Save the file and run the app using the following command:

```dart
flutter run
```

You should now see the app running with a custom shape button group. The buttons will be arranged in a row with a custom shape clipper applied to the container.

## Conclusion

In this tutorial, we learned how to create a custom shape button group using the CustomClipper class in Flutter. By utilizing the CustomPaint widget and ClipPath, we were able to achieve the desired custom shape effect. Feel free to customize the shape and appearance of the button group to fit your app's design.

#flutter #customshape #button #flutterdevelopment