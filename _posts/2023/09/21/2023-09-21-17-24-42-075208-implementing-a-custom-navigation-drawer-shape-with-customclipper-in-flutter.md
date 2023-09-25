---
layout: post
title: "Implementing a custom navigation drawer shape with CustomClipper in Flutter"
description: " "
date: 2023-09-21
tags: [navigationdrawer]
comments: true
share: true
---

Flutter provides a lot of flexibility when it comes to customizing the UI of your app. One area where you can get creative is in modifying the shape of the navigation drawer. In this tutorial, we will learn how to implement a custom navigation drawer shape using the `CustomClipper` widget in Flutter.

## Prerequisites

Before we get started, make sure you have Flutter installed on your machine. You can follow the official [Flutter installation guide](https://flutter.dev/docs/get-started/install) for detailed instructions on how to set it up.

## Step 1: Creating a new Flutter project

Let's start by creating a new Flutter project. Open your favorite terminal and run the following command:

```dart
flutter create custom_navigation_drawer
```

This will create a new Flutter project named `custom_navigation_drawer`.

## Step 2: Setting up the project

Once the project is created, navigate to the project directory:

```dart
cd custom_navigation_drawer
```

Next, open the project in your favorite code editor.

## Step 3: Modifying the main.dart file

Open the `lib/main.dart` file and modify it as follows:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(CustomNavigationDrawerApp());
}

class CustomNavigationDrawerApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Custom Navigation Drawer',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: HomeScreen(),
    );
  }
}

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Home'),
      ),
      drawer: CustomDrawer(),
      body: Center(
        child: Text(
          'Welcome to Custom Navigation Drawer!',
          style: TextStyle(fontSize: 20),
        ),
      ),
    );
  }
}

class CustomDrawer extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ClipPath(
      clipper: OvalRightBorderClipper(),
      child: Drawer(
        child: ListView(
          children: [
            ListTile(
              leading: Icon(Icons.home),
              title: Text('Home'),
              onTap: () {
                // handle drawer item tap
              },
            ),
            ListTile(
              leading: Icon(Icons.settings),
              title: Text('Settings'),
              onTap: () {
                // handle drawer item tap
              },
            ),
          ],
        ),
      ),
    );
  }
}

class OvalRightBorderClipper extends CustomClipper<Path> {
  @override
  Path getClip(Size size) {
    Path path = Path();
    double width = size.width;
    double height = size.height;
    double xPoint = width - 40;

    path.lineTo(width, 0);
    path.quadraticBezierTo(width, 0, width, height / 2);
    path.quadraticBezierTo(width, height, xPoint, height);
    path.lineTo(0, height);
    path.lineTo(0, 0);

    return path;
  }

  @override
  bool shouldReclip(CustomClipper<Path> oldClipper) {
    return true;
  }
}
```

## Step 4: Running the app

Save the changes and run the app using the following command:

```dart
flutter run
```

You should now see a basic home screen with a custom navigation drawer shape on the right side of the screen. Tap on the drawer icon to open the custom navigation drawer.

## Conclusion

In this tutorial, we learned how to implement a custom navigation drawer shape using the `CustomClipper` widget in Flutter. Feel free to experiment with different shapes and designs to make your app's navigation drawer stand out.

#flutter #navigationdrawer