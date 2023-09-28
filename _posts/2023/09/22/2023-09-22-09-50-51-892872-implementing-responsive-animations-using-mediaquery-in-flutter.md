---
layout: post
title: "Implementing responsive animations using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [responsive]
comments: true
share: true
---

With the growing popularity of mobile devices with different screen sizes and orientations, it's essential to create responsive user interfaces for your Flutter apps. One aspect of creating responsive UIs is implementing animations that adapt to different device sizes.

A powerful tool in Flutter for creating responsive animations is the `MediaQuery` class. `MediaQuery` provides access to the device's screen size and other important information, allowing you to make your animations adjust dynamically based on the available space.

Here's an example of how to implement responsive animations using `MediaQuery` in Flutter:

## Step 1: Import the required packages

Make sure you have imported the necessary packages for your Flutter project:

```dart
import 'package:flutter/material.dart';
```

## Step 2: Create a StatefulWidget

To create an animated widget that responds to changes in `MediaQuery`, you'll need to create a StatefulWidget. Let's create a simple example where a container's width changes based on the device's orientation:

```dart
class ResponsiveAnimationWidget extends StatefulWidget {
  @override
  _ResponsiveAnimationWidgetState createState() =>
      _ResponsiveAnimationWidgetState();
}
```

## Step 3: Implement the State class

In the State class, we'll use the `initState` method to initialize a listener to the `MediaQuery` changes. Whenever the device orientation changes, we'll update the container's width accordingly:

```dart
class _ResponsiveAnimationWidgetState extends State<ResponsiveAnimationWidget> {
  double _containerWidth = 200.0;

  @override
  void initState() {
    super.initState();
    MediaQuery.of(context).addListener(() {
      setState(() {
        _containerWidth = MediaQuery.of(context).size.width * 0.5;
      });
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Responsive Animation'),
      ),
      body: Center(
        child: AnimatedContainer(
          duration: Duration(milliseconds: 500),
          width: _containerWidth,
          height: 200.0,
          color: Colors.blue,
        ),
      ),
    );
  }
}
```

In the `initState` method, we add a listener to the `MediaQuery` using `addListener`. When the device orientation changes, the `setState` method is called, updating the `_containerWidth` with a new value based on the updated screen size.

In the `build` method, we use `AnimatedContainer` to create a container that animates its width changes. The `AnimatedContainer` automatically animates whenever we change the width value of `_containerWidth`.

## Step 4: Use the responsive animation widget

Finally, use the `ResponsiveAnimationWidget` in your app's main widget hierarchy:

```dart
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Responsive Animation Example',
      home: ResponsiveAnimationWidget(),
    );
  }
}
```

## Conclusion

Using `MediaQuery` in Flutter allows you to create responsive animations that adapt to different device sizes and orientations. By leveraging the device's screen size information, your app's UI can provide a consistent and smooth user experience across various devices.

#flutter #responsive #animations