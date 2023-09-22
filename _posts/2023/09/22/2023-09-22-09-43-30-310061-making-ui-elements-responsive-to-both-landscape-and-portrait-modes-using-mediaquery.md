---
layout: post
title: "Making UI elements responsive to both landscape and portrait modes using `MediaQuery`"
description: " "
date: 2023-09-22
tags: [flutter, responsiveUI]
comments: true
share: true
---
## Learn how to create a responsive user interface using the `MediaQuery` class

In today's increasingly mobile world, **creating responsive user interfaces** that adapt to different device orientations is crucial. Users expect applications to provide a seamless experience, whether they are using their devices in landscape or portrait mode.

In this blog post, we will explore how to make UI elements responsive to both landscape and portrait modes using the `MediaQuery` class in your preferred programming language.

## What is `MediaQuery`?
`MediaQuery` is a powerful concept that allows you to apply different styles or behaviors to your UI based on the specific media features of the device it is being displayed on.

Some common media features include the screen size, orientation, resolution, and more. By leveraging `MediaQuery`, you can create dynamic and adaptable UIs that respond to various device configurations.

## Using `MediaQuery` for Responsive UI
To make your UI elements responsive to both landscape and portrait modes, follow these steps:

1. Determine the responsive behavior you want for your UI elements in portrait and landscape modes.

2. Create two separate styles for each mode.

3. Wrap your UI elements that need to be responsive with a `MediaQuery` widget.

4. Specify the corresponding `orientation` media query based on the mode you want to apply the styles to.

Here's an example code snippet in **Flutter**:

```dart
import 'package:flutter/material.dart';

class ResponsiveScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MediaQuery(
      data: MediaQuery.of(context).copyWith(
        // Portrait mode style
        textScaleFactor: 1.0,
        // Landscape mode style
        textScaleFactor: 1.2,
      ),
      child: YourUIWidget(),
    );
  }
}

class YourUIWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      child: Text(
        'Responsive UI Example',
        style: TextStyle(fontSize: MediaQuery.of(context).textScaleFactor * 20),
      ),
    );
  }
}

void main() {
  runApp(
    MaterialApp(
      home: ResponsiveScreen(),
    ),
  );
}
```
In the above code, we wrap the `YourUIWidget` with a `MediaQuery` widget and specify two different values for the `textScaleFactor` media query. The `textScaleFactor` determines the font scaling behavior for the text based on the device's orientation.

By providing different values for `textScaleFactor` in portrait and landscape modes, we can achieve a responsive font size across different orientations.

## Conclusion

Creating a responsive user interface is crucial for a seamless user experience across different device orientations. By utilizing the `MediaQuery` class, you can easily adapt your UI elements to fit both landscape and portrait modes.

Remember to test your UI in different orientations to ensure optimal performance and adaptability. With responsive UI, you can provide a consistent and user-friendly experience to your app users.

#flutter #responsiveUI