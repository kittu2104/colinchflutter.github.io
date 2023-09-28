---
layout: post
title: "Using CustomClipper to create a custom swipe card shape in Flutter"
description: " "
date: 2023-09-21
tags: [CustomClipper]
comments: true
share: true
---

![swipe_card](image link)

Creating custom shapes in Flutter can easily be achieved by using the `CustomClipper` class. In this tutorial, we will explore how to use `CustomClipper` to create a custom swipe card shape, like the one shown in the image above.

## Prerequisites

Before proceeding, make sure you have Flutter installed on your machine. If not, refer to the official Flutter documentation for installation instructions.

## Implementation

1. Create a new Flutter project and open the `main.dart` file.

2. Import the required packages:
```dart
import 'package:flutter/material.dart';
```

3. Create a class for our custom clipper:
```dart
class CustomSwipeCardClipper extends CustomClipper<Path> {
  @override
  Path getClip(Size size) {
    final path = Path();

    // Set the starting point of the path
    path.moveTo(size.width * 0.35, 0);

    // Create the card shape by adding curves and lines
    path.quadraticBezierTo(size.width * 0.20, size.height * 0.08, 0, size.height * 0.35);
    path.lineTo(0, size.height * 0.65);
    path.quadraticBezierTo(size.width * 0.20, size.height * 0.92, size.width * 0.35, size.height);
    path.lineTo(size.width * 0.65, size.height);
    path.quadraticBezierTo(size.width * 0.80, size.height * 0.92, size.width, size.height * 0.65);
    path.lineTo(size.width, size.height * 0.35);
    path.quadraticBezierTo(size.width * 0.80, size.height * 0.08, size.width * 0.65, 0);
    path.close();

    return path;
  }

  @override
  bool shouldReclip(CustomSwipeCardClipper oldClipper) => false;
}
```

In the `getClip` method, we define the custom shape of our swipe card using the `Path` class. The `quadraticBezierTo` method allows us to create curves, while the `lineTo` method creates lines to connect the curves.

The `shouldReclip` method is overridden to return `false` since we don't need to update the clipper shape dynamically.

4. In the `build` method of the `MyApp` class, use the `ClipPath` widget to apply the custom clipper to a container:
```dart
ClipPath(
  clipper: CustomSwipeCardClipper(),
  child: Container(
    // Add your card content here
  ),
),
```

The `clipper` property of the `ClipPath` widget takes an instance of our custom clipper class.

5. Run the application using `flutter run` command and you should see the custom swipe card shape.

## Conclusion

In this tutorial, we learned how to use the `CustomClipper` class to create a custom swipe card shape in Flutter. With Flutter's robust drawing capabilities, the possibilities of creating unique and visually appealing UI elements are endless.

#flutter #CustomClipper