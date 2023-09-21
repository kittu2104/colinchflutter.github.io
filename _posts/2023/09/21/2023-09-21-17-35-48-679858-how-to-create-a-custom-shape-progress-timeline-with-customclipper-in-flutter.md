---
layout: post
title: "How to create a custom shape progress timeline with CustomClipper in Flutter"
description: " "
date: 2023-09-21
tags: [flutter, customshape, progress, timeline, dart]
comments: true
share: true
---

Flutter provides a powerful widget called `CustomPaint` that allows you to create custom shapes and drawings on the canvas. With the help of `CustomClipper` class, you can define a custom clipper that clips the widget to a specific shape.

In this tutorial, we will learn how to create a custom shape progress timeline using `CustomClipper` in Flutter.

## Step 1: Set up a Flutter project

Before we start, make sure you have Flutter installed and set up on your system. If not, head over to the official Flutter website and follow the installation instructions.

## Step 2: Create a new Flutter project

Open your terminal or command prompt and run the following command to create a new Flutter project:

```bash
$ flutter create custom_shape_progress_timeline
```

## Step 3: Create a custom shape clipper

In the `lib` folder of your Flutter project, create a new Dart file called `custom_clipper.dart`. In this file, we will define our custom shape clipper.

```dart
import 'package:flutter/material.dart';

class CustomShapeClipper extends CustomClipper<Path> {
  @override
  Path getClip(Size size) {
    final path = Path();

    // Define the shape of the progress timeline
    path.moveTo(0, size.height / 2);
    path.lineTo(0, size.height);
    path.lineTo(size.width, size.height);
    path.lineTo(size.width, size.height / 2);

    return path;
  }

  @override
  bool shouldReclip(CustomClipper<Path> oldClipper) => false;
}
```
## Step 4: Implement the custom shape progress timeline

Next, open the `lib/main.dart` file and replace the code with the following:

```dart
import 'package:flutter/material.dart';
import 'custom_clipper.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Custom Shape Progress Timeline',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Custom Shape Progress Timeline'),
        ),
        body: Center(
          child: Container(
            height: 100, // Adjust the height as per your requirements
            child: ClipPath(
              clipper: CustomShapeClipper(),
              child: LinearProgressIndicator(
                value: 0.75, // Adjust the value to show the progress
                backgroundColor: Colors.grey,
                valueColor: AlwaysStoppedAnimation<Color>(Colors.blue),
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```

## Step 5: Run the application

Save the files and run the application using the following command:

```bash
$ flutter run
```

You should now see a custom shape progress timeline with a linear progress indicator based on the custom clipper defined in the `CustomShapeClipper` class.

## Conclusion

In this tutorial, we have learned how to create a custom shape progress timeline using `CustomClipper` in Flutter. You can customize the shape by modifying the code in the `getClip()` method of the `CustomShapeClipper` class. Experiment with different shapes and styles to create unique progress indicators for your Flutter applications.

Give it a try and unleash your creativity with custom shapes in Flutter!

#flutter #customshape #progress #timeline #dart