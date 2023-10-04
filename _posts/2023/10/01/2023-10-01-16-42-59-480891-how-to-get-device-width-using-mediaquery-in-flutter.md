---
layout: post
title: "How to get device width using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [mediadevice]
comments: true
share: true
---

Mobile app development often requires retrieving the dimensions of the device's screen. In Flutter, we can use the `MediaQuery` class to access device information and retrieve the device's width.

## Step 1: Import the necessary packages

First, we need to import the `flutter` package, which includes the `MaterialApp` class. Additionally, we'll import the `package:flutter/widgets.dart` package to access the `MediaQuery` class.

```dart
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';
```

## Step 2: Retrieve the device's width

To get the device's width, we can use `MediaQuery.of(context).size.width`. Here's an example of how to retrieve the device's width and use it in a Flutter widget:

```dart
class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    double deviceWidth = MediaQuery.of(context).size.width;

    return Container(
      width: deviceWidth,
      height: 200,
      color: Colors.blue,
      child: Text('Device Width: $deviceWidth'),
    );
  }
}
```

In the above code, we define a stateless widget called `MyWidget`. Inside the `build` method, we retrieve the device's width using `MediaQuery.of(context).size.width` and store it in the `deviceWidth` variable.

We then use this `deviceWidth` value to set the width of the `Container` widget, which will be the same as the device's width. We also display the `deviceWidth` value within the widget by wrapping a `Text` widget inside the `Container`.

## Step 3: Use the widget in the app

To use the `MyWidget` widget in your Flutter app, include it within the `build` method of your `MaterialApp`:

```dart
void main() {
  runApp(MaterialApp(
    home: Scaffold(
      appBar: AppBar(
        title: Text('Device Width Example'),
      ),
      body: MyWidget(),
    ),
  ));
}
```

In the above code, we define the `main` function that calls the `runApp` method, which wraps the `MaterialApp` widget. Inside the `Scaffold` widget, we include the `MyWidget` using the `body` parameter.

Now, when you run your app, the `MyWidget` widget will display the device's width within a blue-colored container.

By utilizing the `MediaQuery` class in Flutter, we can easily retrieve the device's width and use it within our app for creating responsive layouts or adapting to different screen sizes.

#flutter #mediadevice