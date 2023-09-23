---
layout: post
title: "Creating a responsive animated button using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [flutter, flutterdev]
comments: true
share: true
---

In this tutorial, we will learn how to create a responsive animated button using `MediaQuery` in Flutter. The button will adjust its size and animation based on the screen size, allowing for a smooth, seamless user experience on different devices.

## Step 1: Set up a Flutter project

Before we begin, make sure you have Flutter installed and set up on your machine. You can follow the official Flutter documentation to install and configure Flutter.

## Step 2: Add dependencies

Open your Flutter project and navigate to the `pubspec.yaml` file. Add the following dependency:

```yaml
dependencies:
  flutter:
    sdk: flutter

  animated_text_kit: ^4.2.1
```

Save the file and run `flutter pub get` to fetch the dependency.

## Step 3: Implement MediaQuery

To make the button responsive, we will use the `MediaQuery` widget in Flutter. MediaQuery allows us to retrieve information about the current device's screen, such as the screen width and height, and adjust our UI accordingly.

First, import the following packages in your Dart file:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/rendering.dart';
```

Next, create a `StatefulWidget` called `ResponsiveButton` and define its state. In the state class, add the following code:

```dart
class _ResponsiveButtonState extends State<ResponsiveButton> {
  bool _isPressed = false;
  double _buttonWidth = 200.0;
  double _buttonHeight = 50.0;

  @override
  Widget build(BuildContext context) {
    double screenWidth = MediaQuery.of(context).size.width;
    if (screenWidth < 600) {
      _buttonWidth = 150.0;
      _buttonHeight = 35.0;
    }

    return GestureDetector(
      onTapDown: (TapDownDetails details) {
        setState(() {
          _isPressed = true;
        });
      },
      onTapUp: (TapUpDetails details) {
        setState(() {
          _isPressed = false;
        });
      },
      child: AnimatedContainer(
        duration: Duration(milliseconds: 200),
        width: _isPressed ? (_buttonWidth - 10.0) : _buttonWidth,
        height: _isPressed ? (_buttonHeight - 10.0) : _buttonHeight,
        decoration: BoxDecoration(
          color: Colors.blue,
          borderRadius: BorderRadius.circular(8.0),
          boxShadow: [
            BoxShadow(
              color: Colors.grey.withOpacity(0.5),
              spreadRadius: 2,
              blurRadius: 5,
              offset: Offset(0, 2),
            ),
          ],
        ),
        child: Center(
          child: Text(
            _isPressed ? 'Button Pressed' : 'Press Me',
            style: TextStyle(
              color: Colors.white,
              fontSize: 16.0,
            ),
          ),
        ),
      ),
    );
  }
}
```

## Step 4: Use the ResponsiveButton widget

In your main widget, you can now use the `ResponsiveButton` widget. Here's an example of how to use it:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Responsive Button Example',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Responsive Button Example'),
        ),
        body: Center(
          child: ResponsiveButton(),
        ),
      ),
    );
  }
}
```

## Step 5: Run the app

Save your changes and run the app using `flutter run`. You should now see a responsive animated button on the screen. Try resizing the application window and observe how the button adjusts its size and animation based on the screen width.

Congratulations! You have successfully created a responsive animated button using MediaQuery in Flutter.

#flutter #flutterdev