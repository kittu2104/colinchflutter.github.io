---
layout: post
title: "Implementing responsive buttons and icons using `MediaQuery`"
description: " "
date: 2023-09-23
tags: [Flutter, ResponsiveUI]
comments: true
share: true
---

In today's digital landscape, creating a responsive user interface is crucial to ensure a seamless experience across devices of varying screen sizes. One essential aspect of a responsive design is the ability to adapt buttons and icons based on the device's screen width. In this blog post, we will explore how to achieve this using the `MediaQuery` widget in Flutter.

## Understanding `MediaQuery`

`MediaQuery` is a powerful Flutter widget that allows us to obtain information about the current device's screen size and orientation. It provides access to various properties such as screen width, height, aspect ratio, and more. This information can be utilized to create responsive UI elements that adapt and scale according to the available screen real estate.

## Implementing Responsive Buttons

Let's start by implementing responsive buttons that adjust their size based on the device's screen width. Here's an example code snippet:

```dart
import 'package:flutter/material.dart';

class ResponsiveButton extends StatelessWidget {
  final String text;
  final Function onPressed;

  const ResponsiveButton({required this.text, required this.onPressed});

  @override
  Widget build(BuildContext context) {
    final screenSize = MediaQuery.of(context).size;
    final buttonWidth = screenSize.width < 600 ? 150.0 : 250.0;

    return Container(
      width: buttonWidth,
      height: 50.0,
      child: ElevatedButton(
        onPressed: onPressed,
        child: Text(text),
      ),
    );
  }
}
```

In this code, we use the `MediaQuery` widget to retrieve the device's screen size (`screenSize`). We then define a `buttonWidth` variable that adapts based on the screen width. If the screen width is less than 600 pixels, we set the button width to 150 pixels; otherwise, we set it to 250 pixels. This ensures that the button scales appropriately on different devices.

## Implementing Responsive Icons

Similarly, we can make icons responsive by adjusting their size based on the device's screen width. Here's an example code snippet demonstrating this:

```dart
import 'package:flutter/material.dart';

class ResponsiveIcon extends StatelessWidget {
  final IconData iconData;

  const ResponsiveIcon({required this.iconData});

  @override
  Widget build(BuildContext context) {
    final screenSize = MediaQuery.of(context).size;
    final iconSize = screenSize.width < 600 ? 20.0 : 30.0;

    return Icon(
      iconData,
      size: iconSize,
    );
  }
}
```

In this code, we use the `MediaQuery` widget to retrieve the device's screen size (`screenSize`). We define an `iconSize` variable that adjusts based on the screen width. If the screen width is less than 600 pixels, we set the icon size to 20 pixels; otherwise, we set it to 30 pixels. This ensures that the icon remains proportionate across different devices.

## Conclusion

By utilizing the power of the `MediaQuery` widget in Flutter, we can easily create responsive buttons and icons that adapt to different screen sizes. This allows us to provide users with a consistent and visually appealing experience regardless of the device they are using. So go ahead, implement responsive design in your Flutter applications and elevate the user experience to new heights!

#Flutter #ResponsiveUI