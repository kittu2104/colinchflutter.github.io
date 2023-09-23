---
layout: post
title: "Building a responsive layout using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [Flutter, ResponsiveLayout]
comments: true
share: true
---

In this tutorial, we will learn how to create a responsive layout in Flutter using the `MediaQuery` class. Flutter provides a flexible and powerful way to build responsive user interfaces that adapt to different screen sizes and orientations.

## What is MediaQuery?

`MediaQuery` is a class in Flutter that provides information about the current device's size, orientation, and pixel density. It allows us to create layouts that can adapt to different device configurations, providing a consistent user experience across different screens.

## Getting Started

To get started, create a new Flutter project or open an existing one. Open the main.dart file and remove the default code. We will start from scratch.

## Step 1: Import the required packages

First, let's import the necessary packages for our project. We will need the `material` package for the Flutter material design widgets and `cupertino` package for the iOS-style widgets.

```dart
import 'package:flutter/material.dart';
import 'package:flutter/cupertino.dart';
```

## Step 2: Create the main widget

Next, let's create the main widget for our application. We will use a `StatefulWidget` as our root widget.

```dart
class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Responsive Layout',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Responsive Layout'),
        ),
        body: Container(
          // Add your layout widgets here
        ),
      ),
    );
  }
}
```

## Step 3: Add responsive layout

Inside the `body` property of the `Scaffold` widget, we can add our responsive layout. Let's use a `Column` widget as an example.

```dart
body: Container(
  child: Column(
    children: [
      Text(
        'Welcome to the Responsive Layout',
        style: TextStyle(fontSize: 20),
      ),
      SizedBox(height: 10),
      Text(
        'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',
        style: TextStyle(fontSize: 16),
      ),
    ],
  ),
),
```

## Step 4: Make the layout responsive

To make the layout responsive, we can use `MediaQuery` class to get the screen dimensions and adjust the layout accordingly. We will wrap our `Column` widget with the `LayoutBuilder` widget.

```dart
body: Container(
  child: LayoutBuilder(
    builder: (BuildContext context, BoxConstraints constraints) {
      if (constraints.maxWidth >= 600) {
        // Layout for larger screens
        return Column(
          children: [
            Text(
              'Welcome to the Responsive Layout',
              style: TextStyle(fontSize: 24),
            ),
            SizedBox(height: 20),
            Text(
              'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',
              style: TextStyle(fontSize: 18),
            ),
          ],
        );
      } else {
        // Layout for smaller screens
        return Column(
          children: [
            Text(
              'Welcome to the Responsive Layout',
              style: TextStyle(fontSize: 20),
            ),
            SizedBox(height: 10),
            Text(
              'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',
              style: TextStyle(fontSize: 16),
            ),
          ],
        );
      }
    },
  ),
),
```

In the above code, we check the `maxWidth` of the layout and choose different font sizes based on the screen width. On larger screens (width >= 600), we display a larger font size, while on smaller screens, we use a smaller font size.

## Step 5: Run the application

Save the changes and run the application on a device or emulator. You will see that the layout adjusts based on the screen size, providing a responsive user interface.

## Summary

In this tutorial, we learned how to build a responsive layout in Flutter using the `MediaQuery` class. We used the `LayoutBuilder` widget to adjust the layout based on the screen dimensions. Building responsive layouts in Flutter allows us to create applications that adapt to different screen sizes and orientations, providing a consistent user experience. #Flutter #ResponsiveLayout