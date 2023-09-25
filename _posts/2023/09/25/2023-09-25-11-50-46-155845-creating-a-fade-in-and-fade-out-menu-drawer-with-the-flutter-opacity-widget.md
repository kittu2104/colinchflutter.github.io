---
layout: post
title: "Creating a fade-in and fade-out menu drawer with the Flutter Opacity widget."
description: " "
date: 2023-09-25
tags: [flutter, animation]
comments: true
share: true
---

In modern app design, menu drawers are a common component used for navigation. Adding subtle animation effects can enhance the user experience and create a more polished look. In this tutorial, we will learn how to create a fade-in and fade-out menu drawer using the Flutter Opacity widget.

## Prerequisites

To follow along with this tutorial, you should have the following:

- Flutter SDK installed
- A basic understanding of Flutter widgets and animations

## Step 1: Setting up the project

First, let's create a new Flutter project:

```dart
$ flutter create fade_menu_drawer
$ cd fade_menu_drawer
```

Next, open the `lib/main.dart` file and replace the default code with the following:

```dart
import 'package:flutter/material.dart';

void main() => runApp(FadeMenuDrawerApp());

class FadeMenuDrawerApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: FadeMenuDrawer(),
    );
  }
}

class FadeMenuDrawer extends StatefulWidget {
  @override
  _FadeMenuDrawerState createState() => _FadeMenuDrawerState();
}

class _FadeMenuDrawerState extends State<FadeMenuDrawer>
    with SingleTickerProviderStateMixin {
  AnimationController _animationController;
  bool _isDrawerOpen = false;

  @override
  void initState() {
    super.initState();
    _animationController = AnimationController(
      vsync: this,
      duration: Duration(milliseconds: 300),
    );
  }

  @override
  void dispose() {
    _animationController.dispose();
    super.dispose();
  }

  void _toggleDrawer() {
    setState(() {
      _isDrawerOpen = !_isDrawerOpen;

      if (_isDrawerOpen) {
        _animationController.forward();
      } else {
        _animationController.reverse();
      }
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Stack(
        children: [
          Container(
            color: Colors.white,
          ),
          Opacity(
            opacity: _isDrawerOpen ? 0.5 : 1,
            child: GestureDetector(
              onTap: _toggleDrawer,
              child: Container(
                color: Colors.black,
              ),
            ),
          ),
          SlideTransition(
            position: Tween<Offset>(
              begin: Offset(-1, 0),
              end: Offset(0, 0),
            ).animate(CurvedAnimation(
              parent: _animationController,
              curve: Curves.easeInOut,
            )),
            child: Container(
              width: 200,
              color: Colors.grey[200],
              child: ListView(
                children: [
                  ListTile(
                    title: Text('Item 1'),
                  ),
                  ListTile(
                    title: Text('Item 2'),
                  ),
                  ListTile(
                    title: Text('Item 3'),
                  ),
                ],
              ),
            ),
          ),
        ],
      ),
    );
  }
}
```

## Step 2: Understanding the code

Let's go through the key parts of the code:

1. We create a `FadeMenuDrawer` widget which is the main widget in our application.

2. Inside the `FadeMenuDrawer` widget, we define a `_FadeMenuDrawerState` class which extends `StatefulWidget` and implements `SingleTickerProviderStateMixin`.

3. In the `_FadeMenuDrawerState` class, we create an `AnimationController` to control the animation with a duration of 300 milliseconds.

4. The `_toggleDrawer` method is called when the user taps on the screen. It updates the `_isDrawerOpen` variable and animates the menu drawer based on its state.

5. The `build` method of `_FadeMenuDrawerState` contains the main UI of our app. We use a `Stack` to overlay the menu drawer on top of a background container. The opacity of the background container is controlled based on whether the drawer is open or not. The menu drawer is animated using `SlideTransition` and `Tween` to create a smooth transition effect.

## Step 3: Running the app

To run the app, execute the following command in the terminal:

```dart
$ flutter run
```

You should now see the fade-in and fade-out menu drawer in action. Try tapping on the screen to open and close the drawer.

## Conclusion

In this tutorial, we have learned how to create a fade-in and fade-out menu drawer using the Flutter Opacity widget. Adding animation effects to user interfaces can greatly improve the overall user experience. Feel free to experiment with different animations and customize the menu drawer to suit your app's design.

Give it a try and enjoy creating beautiful and interactive Flutter apps!

#flutter #animation