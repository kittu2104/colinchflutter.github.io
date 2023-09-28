---
layout: post
title: "Navigating between screens in a StatelessWidget in Flutter"
description: " "
date: 2023-09-24
tags: [navigations]
comments: true
share: true
---

When building a Flutter application, it is common to have multiple screens or pages to provide a smooth and interactive user experience. In Flutter, navigating between screens can be easily achieved using the **Navigator** class. In this blog post, we will explore how to navigate between screens in a **StatelessWidget**.

## Step 1: Import the required packages

Before we get started, let's make sure we have the necessary packages imported in our **pubspec.yaml** file.

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter/material.dart:
  flutter/widgets.dart:
```

## Step 2: Define the screens

First, let's define two screens that we want to navigate between. For this example, we will create a home screen and a details screen. In the home screen, we will have a button that triggers the navigation to the details screen.

Create two separate files for each screen: **home_screen.dart** and **details_screen.dart**. In each file, create a **StatelessWidget** and define the UI accordingly.

```dart
// home_screen.dart

import 'package:flutter/material.dart';

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Home Screen'),
      ),
      body: Center(
        child: RaisedButton(
          child: Text('Go to Details'),
          onPressed: () {
            // Navigate to details screen
          },
        ),
      ),
    );
  }
}
```

```dart
// details_screen.dart

import 'package:flutter/material.dart';

class DetailsScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Details Screen'),
      ),
      body: Center(
        child: RaisedButton(
          child: Text('Go Back'),
          onPressed: () {
            // Navigate back to home screen
          },
        ),
      ),
    );
  }
}
```

## Step 3: Implement navigation logic

Now that we have our screens defined, let's implement the navigation logic in the **onPressed** callbacks of the buttons.

In the home screen, when the button is pressed, we want to navigate to the details screen. We can achieve this by using the **Navigator.push()** method.

```dart
// home_screen.dart

RaisedButton(
  child: Text('Go to Details'),
  onPressed: () {
    Navigator.push(
      context,
      MaterialPageRoute(builder: (context) => DetailsScreen()),
    );
  },
),
```

In the details screen, when the button is pressed, we want to navigate back to the home screen. We can achieve this by using the **Navigator.pop()** method.

```dart
// details_screen.dart

RaisedButton(
  child: Text('Go Back'),
  onPressed: () {
    Navigator.pop(context);
  },
),
```

## Step 4: Test the navigation

To test the navigation, we need to update the **main.dart** file to set **HomeScreen** as the initial route.

```dart
import 'package:flutter/material.dart';
import 'package:navigation_example/screens/home_screen.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Navigation Example',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: HomeScreen(),
    );
  }
}
```

Now, when you run the application, you should see the home screen with a button. When you tap the button, you should be navigated to the details screen, and when you tap the button in the details screen, you should be navigated back to the home screen.

Congratulations! You have successfully implemented navigation between screens in a **StatelessWidget** in Flutter.

#flutter #navigations