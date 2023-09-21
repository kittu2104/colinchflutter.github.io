---
layout: post
title: "Creating a custom shape chat bubble with tails using CustomClipper in Flutter"
description: " "
date: 2023-09-21
tags: [Flutter, CustomClipper]
comments: true
share: true
---

In this tutorial, we will explore how to create a custom shape chat bubble with tails in Flutter using the `CustomClipper` class. The `CustomClipper` class allows us to customize the shape of a widget by defining a custom clipping path.

## Step 1: Creating a CustomClipper Class

First, we need to create a custom `CustomClipper` class that extends the `CustomClipper<Path>` class. This class will be responsible for defining the custom shape of our chat bubble.

```dart
import 'package:flutter/material.dart';

class ChatBubbleClipper extends CustomClipper<Path> {
  @override
  Path getClip(Size size) {
    Path path = Path();
    // Define your custom shape here
    // Use path.lineTo(), path.quadraticBezierTo(), or path.cubicTo() to create the desired shape
    // Remember to consider the size parameter for the bubble dimensions

    return path;
  }

  @override
  bool shouldReclip(ChatBubbleClipper oldClipper) => true;
}
```

## Step 2: Implementing the CustomClipper

Next, we need to implement the `CustomClipper` in our chat bubble widget. We can use the `ClipPath` widget to apply the clipper to our widget.

```dart
ClipPath(
  clipper: ChatBubbleClipper(),
  child: Container(
    // Add your widget contents here
  ),
)
```

## Step 3: Defining the Custom Shape

Inside the `getClip(Size size)` method of the `ChatBubbleClipper` class, we can define the custom shape for our chat bubble. Here's an example of creating a chat bubble shape with a tail on the left:

```dart
Path path = Path();
path.lineTo(0, size.height); // Starting point of the left edge
path.quadraticBezierTo(0, size.height * 0.2, size.width * 0.15, size.height * 0.2); // Top-left curve point
path.lineTo(size.width * 0.75, size.height * 0.2); // Top edge
path.quadraticBezierTo(size.width, size.height * 0.2, size.width, 0); // Top-right curve point
path.lineTo(0, 0); // Starting point of the right edge

return path;
```

Feel free to experiment and customize the shape to your liking. You can use a combination of `lineTo()`, `quadraticBezierTo()`, and `cubicTo()` methods to create more complex shapes.

## Conclusion

In this tutorial, we have learned how to create a custom shape chat bubble with tails in Flutter using the `CustomClipper` class. By defining a custom clipping path, we can create unique and visually appealing chat bubbles for our Flutter applications.

Give it a try and unleash your creativity in designing chat bubbles that perfectly fit your app's style!

#Flutter #CustomClipper