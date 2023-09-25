---
layout: post
title: "Creating a responsive rating bar using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [responsive, ratingbar]
comments: true
share: true
---

In this tutorial, we will learn how to create a responsive rating bar using `MediaQuery` in Flutter. The `MediaQuery` class allows us to access information about the current device's size and orientation, which is useful for creating UI elements that adapt to different screen sizes.

## Prerequisites

Make sure you have Flutter installed on your system and a basic understanding of Flutter widgets and layouts.

## Step 1: Set up a Flutter project

Open your terminal and run the following command to create a new Flutter project:

```bash
flutter create responsive_rating_bar
```

## Step 2: Create a new Flutter widget

Navigate to the `lib` folder of your project and create a new file called `rating_bar.dart`. In this file, we will define our `RatingBar` widget.

```dart
import 'package:flutter/material.dart';

class RatingBar extends StatelessWidget {
  final int rating;
  final Color fillColor;
  final double size;

  const RatingBar({
    Key? key,
    required this.rating,
    required this.fillColor,
    required this.size,
  }) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Row(
      mainAxisAlignment: MainAxisAlignment.center,
      children: List.generate(
        5,
        (index) => Icon(
          index < rating ? Icons.star : Icons.star_border,
          color: fillColor,
          size: size,
        ),
      ),
    );
  }
}
```

## Step 3: Use the `RatingBar` widget

Let's use the `RatingBar` widget in our main Flutter app. Open the `lib/main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';
import 'rating_bar.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Responsive Rating Bar',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Responsive Rating Bar'),
        ),
        body: Center(
          child: MediaQuery.of(context).size.width < 600
              ? RatingBar(
                  rating: 3,
                  fillColor: Colors.amber,
                  size: 40.0,
                )
              : RatingBar(
                  rating: 4,
                  fillColor: Colors.amber,
                  size: 60.0,
                ),
        ),
      ),
    );
  }
}
```

The `MediaQuery.of(context).size.width` is used to check the width of the device's screen. If the screen width is less than `600`, we display a smaller rating bar with a size of `40.0`. Otherwise, we display a larger rating bar with a size of `60.0`.

## Step 4: Run the app

Save the changes and run the app using the following command:

```bash
flutter run
```

You should now see the app running with a responsive rating bar based on the device's screen width.

## Conclusion

In this tutorial, we learned how to create a responsive rating bar using `MediaQuery` in Flutter. By leveraging the screen size information provided by `MediaQuery`, we were able to create a UI element that adapts to different screen sizes. With this knowledge, you can create more flexible and user-friendly Flutter apps. Happy coding!

#flutter #responsive #ratingbar