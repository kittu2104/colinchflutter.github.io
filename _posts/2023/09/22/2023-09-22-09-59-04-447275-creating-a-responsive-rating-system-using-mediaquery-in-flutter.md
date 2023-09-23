---
layout: post
title: "Creating a responsive rating system using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: []
comments: true
share: true
---

Flutter is a powerful framework for building cross-platform mobile applications. One of its key features is the ability to create responsive user interfaces that adapt to different screen sizes and orientations. In this blog post, we will explore how to create a responsive rating system using the `MediaQuery` class in Flutter.

## What is MediaQuery?

In Flutter, `MediaQuery` is a class that provides access to the media information, such as the screen size, orientation, and pixel density. It allows us to create responsive layouts that adjust dynamically based on the available screen space.

## Implementing the Rating System

To create a responsive rating system, we will use the `MediaQuery` class to determine the screen width and adjust the layout accordingly. Let's go through the step-by-step process.

### Step 1: Setting up the Project

Create a new Flutter project by running the following command in your terminal:

```bash
flutter create responsive_rating_system
```

### Step 2: Setting up the Rating Widget

In the `lib/main.dart` file, replace the default `MyApp` class with the following code:

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Responsive Rating System',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: RatingScreen(),
    );
  }
}

class RatingScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Rating System'),
      ),
      body: Center(
        child: Text(
          'Rating System Widget',
          style: TextStyle(fontSize: 20.0),
        ),
      ),
    );
  }
}
```

### Step 3: Creating a Responsive Layout

Update the `RatingScreen` widget to include a responsive layout using `MediaQuery`. Replace the `RatingScreen` class with the following code:

```dart
class RatingScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final screenWidth = MediaQuery.of(context).size.width;

    return Scaffold(
      appBar: AppBar(
        title: Text('Rating System'),
      ),
      body: Center(
        child: Container(
          width: screenWidth * 0.8, // Adjust the width based on screen size
          height: 200.0,
          color: Colors.grey[200],
          child: Center(
            child: Text(
              'Rating System Widget',
              style: TextStyle(fontSize: 20.0),
            ),
          ),
        ),
      ),
    );
  }
}
```

In the code above, we use `MediaQuery.of(context).size.width` to fetch the screen width. We then set the width of the rating container to 80% of the screen width, making it responsive across different devices or orientations.

### Step 4: Adding the Rating Icons

To make our rating system more interactive, we can add rating icons such as stars or hearts. We won't go into the details of adding icons in this blog post, but you can use Flutter's `Icon` widget along with gesture detection to handle user interactions.

### Step 5: Testing the Rating System

Save the changes and run your app using:

```bash
flutter run
```

You should see the rating system widget displayed, with a responsive layout that adapts to different screen sizes.

## Conclusion

In this blog post, we explored how to create a responsive rating system using the `MediaQuery` class in Flutter. By leveraging the screen information provided by `MediaQuery`, we can create layouts that adapt to different screen sizes and provide a consistent user experience across various devices and orientations.