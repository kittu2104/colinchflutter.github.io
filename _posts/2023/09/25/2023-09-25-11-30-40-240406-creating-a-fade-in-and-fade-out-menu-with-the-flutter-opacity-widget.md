---
layout: post
title: "Creating a fade-in and fade-out menu with the Flutter Opacity widget"
description: " "
date: 2023-09-25
tags: [flutter, opacity]
comments: true
share: true
---

Flutter is a popular framework for building beautiful and responsive mobile applications. One of the common UI effects that developers often want to achieve is creating a fade-in and fade-out menu. This effect can be achieved using the `Opacity` widget in Flutter.

In this tutorial, we will walk you through the steps to create a fade-in and fade-out menu in Flutter using the `Opacity` widget.

### Step 1: Setting up the Project

First, let's create a new Flutter project. Open your preferred IDE and create a new Flutter project using the following command:

```dart
$ flutter create fade_menu
```

### Step 2: Adding the Opacity Widget

Open the `lib/main.dart` file in your project and replace the existing code with the following code:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(FadeMenuApp());
}

class FadeMenuApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Fade Menu',
      home: FadeMenu(),
    );
  }
}

class FadeMenu extends StatefulWidget {
  @override
  _FadeMenuState createState() => _FadeMenuState();
}

class _FadeMenuState extends State<FadeMenu> {
  bool _isMenuVisible = false;

  void _toggleMenu() {
    setState(() {
      _isMenuVisible = !_isMenuVisible;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Fade Menu'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            RaisedButton(
              onPressed: _toggleMenu,
              child: Text(_isMenuVisible ? 'Hide Menu' : 'Show Menu'),
            ),
            Opacity(
              opacity: _isMenuVisible ? 1.0 : 0.0,
              duration: Duration(milliseconds: 500),
              child: Container(
                margin: EdgeInsets.symmetric(vertical: 20.0),
                height: 200.0,
                width: 200.0,
                color: Colors.blue,
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

### Step 3: Running the App

Save the changes and run the app using the following command:

```dart
$ flutter run
```

This will launch the app on your connected device or emulator.

### Step 4: Testing the Fade-In and Fade-Out Menu

Now, when you run the app, you will see a "Show Menu" button on the screen. Pressing this button will fade-in the menu container with a blue background color. Pressing the button again will fade-out the menu.

Congratulations! You have successfully created a fade-in and fade-out menu in Flutter using the `Opacity` widget. Feel free to customize the menu further and add any additional functionality that you desire.

For more advanced UI effects and animations, Flutter provides a wide range of animation widgets and packages that you can explore.

#flutter #opacity #fade-in #fade-out