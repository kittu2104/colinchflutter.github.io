---
layout: post
title: "Creating a responsive rating bar using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [flutter, flutterdevelopment]
comments: true
share: true
---

In this tutorial, we will learn how to create a responsive rating bar in Flutter using `MediaQuery`. A rating bar is a commonly used UI component that allows users to rate or give feedback on something, such as a product or service, by selecting a certain number of stars. By using `MediaQuery`, we can easily make the rating bar adjust its size and layout according to different device screen sizes.

Let's get started!

## Step 1: Set up a new Flutter project

Create a new Flutter project by running the following command in your terminal:

```dart
flutter create responsive_rating_bar
```

## Step 2: Implement the `RatingBar` widget

Open the `lib/main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';

class RatingBar extends StatelessWidget {
  final int starCount;
  final double rating;
  final double size;

  RatingBar({this.starCount = 5, this.rating = 0.0, this.size = 24.0});

  @override
  Widget build(BuildContext context) {
    final double _starSize = size;
    final double _rating = rating.clamp(0.0, starCount.toDouble());

    return Row(
      mainAxisSize: MainAxisSize.min,
      children: List.generate(
        starCount,
        (index) => Icon(
          index < _rating.floor() ? Icons.star : Icons.star_border,
          size: _starSize,
        ),
      ),
    );
  }
}

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
                  size: 60.0,
                )
              : RatingBar(
                  size: 120.0,
                ),
        ),
      ),
    );
  }
}
```

In this code, we have defined a `RatingBar` widget that accepts three optional parameters: `starCount` (number of stars to show), `rating` (current rating value), and `size` (size of each star).

The `build` method of the `RatingBar` widget generates a row of stars using the `Icon` widget. The `rating` value is clamped to ensure it falls within the range of 0.0 to `starCount.toDouble()`. If the device's screen width is less than 600 pixels, a smaller size of rating bar is shown; otherwise, a larger size of rating bar is shown.

In the `MyApp` widget, we set up the Flutter app and define the `Scaffold` with an `AppBar` and `body` that displays the rating bar in the center. The size of the rating bar is dynamically determined using `MediaQuery.of(context).size.width` to check the device's screen width.

## Step 3: Run the app

Save the changes and run the app using the following command:

```dart
flutter run
```

The app should now launch on your device or emulator, and you will see a rating bar displayed in the center of the screen with a size that adapts to the screen width.

## Conclusion

In this tutorial, we have learned how to create a responsive rating bar in Flutter using `MediaQuery`. By leveraging `MediaQuery`, we can easily make our UI components adapt to different device screen sizes, providing a better user experience across a variety of devices. Feel free to customize the rating bar implementation to fit your specific needs and design preferences.

#flutter #flutterdevelopment