---
layout: post
title: "Creating a responsive animated button using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [responsive]
comments: true
share: true
---

Creating responsive UIs is crucial in modern app development, as users access applications on a variety of devices with different screen sizes. In this tutorial, we will learn how to create a responsive animated button using `MediaQuery` in Flutter.

## Prerequisites
Before getting started, make sure you have Flutter installed on your system. If not, you can follow the official Flutter installation guide to set up your development environment.

## Step 1: Set up a new Flutter project
Create a new Flutter project by running the following command in your terminal or command prompt:

```dart
flutter create animated_button
```

Navigate to the project directory:

```dart
cd animated_button
```

## Step 2: Add dependencies
Open the `pubspec.yaml` file in your project and add the following dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter

  cupertino_icons: ^0.1.3
```

Save the file and run the following command to fetch the added dependencies:

```dart
flutter pub get
```

## Step 3: Replace the default code
Replace the default code in the `lib/main.dart` file with the following code:

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Animated Button',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  bool _isButtonPressed = false;

  void _toggleButtonState() {
    setState(() {
      _isButtonPressed = !_isButtonPressed;
    });
  }

  @override
  Widget build(BuildContext context) {
    final screenWidth = MediaQuery.of(context).size.width;

    return Scaffold(
      appBar: AppBar(
        title: Text('Animated Button'),
      ),
      body: Center(
        child: InkWell(
          onTap: _toggleButtonState,
          onTapDown: (details) {
            setState(() {
              _isButtonPressed = true;
            });
          },
          onTapUp: (details) {
            setState(() {
              _isButtonPressed = false;
            });
          },
          onTapCancel: () {
            setState(() {
              _isButtonPressed = false;
            });
          },
          child: AnimatedContainer(
            duration: Duration(milliseconds: 200),
            width: _isButtonPressed ? screenWidth * 0.9 : screenWidth * 0.7,
            height: 50.0,
            alignment: Alignment.center,
            decoration: BoxDecoration(
              borderRadius: BorderRadius.circular(30.0),
              color: _isButtonPressed ? Colors.blue : Colors.grey,
            ),
            child: Text(
              'Press me',
              style: TextStyle(
                color: Colors.white,
                fontWeight: FontWeight.bold,
                fontSize: 16.0,
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```

## Step 4: Run the app
Save the file and run the app using the following command:

```dart
flutter run
```

The app will launch on an emulator or connected device, and you should see a button that animates its size when pressed.

## Conclusion
By using `MediaQuery` in Flutter, we can create responsive UI elements that adapt to the screen size. We have successfully created a responsive animated button that scales its width based on the device screen width. Feel free to customize the button style and explore additional animations to enhance your Flutter apps.

#flutter #UI #responsive #animation