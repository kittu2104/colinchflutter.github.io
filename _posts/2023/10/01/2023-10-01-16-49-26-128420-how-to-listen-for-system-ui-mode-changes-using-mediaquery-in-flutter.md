---
layout: post
title: "How to listen for system UI mode changes using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [Flutter, SystemUIModeChanges]
comments: true
share: true
---

Flutter provides a convenient way to listen for changes in the system UI mode, such as when the device switches between light mode and dark mode. This can be achieved using `MediaQuery`, which is a utility class that provides access to information about the current app and device configuration.

In this blog post, we will explore how to listen for system UI mode changes using `MediaQuery` in Flutter. Let's get started!

## Step 1: Import the necessary packages

First, we need to import the necessary packages to use `MediaQuery` and listen for system UI mode changes. Add the following lines to the top of your Dart file:

```dart
import 'package:flutter/material.dart';
```

## Step 2: Define a StatefulWidget

Next, we need to define a `StatefulWidget` that will handle the UI updates based on the system UI mode changes. Create a new class called `UIChangeListener` that extends `StatefulWidget`:

```dart
class UIChangeListener extends StatefulWidget {
  @override
  _UIChangeListenerState createState() => _UIChangeListenerState();
}
```

## Step 3: Define the State class

Inside the `UIChangeListener` class, define a private class called `_UIChangeListenerState` that extends `State<UIChangeListener>`. This is where we will handle the logic for listening to system UI mode changes:

```dart
class _UIChangeListenerState extends State<UIChangeListener> {
  @override
  Widget build(BuildContext context) {
    return Container(
      // UI components to display based on system UI mode
    );
  }
}
```

## Step 4: Listen for system UI mode changes

In the `_UIChangeListenerState` class, override the `didChangeMetrics` method. This method is called whenever the system UI mode changes. Inside this method, we can update the UI according to the new mode. Add the following code inside the `_UIChangeListenerState` class:

```dart
@override
void didChangeMetrics() {
  super.didChangeMetrics();
  
  // Check the current brightness mode
  final brightness = MediaQuery.of(context).platformBrightness;

  // Update the UI based on brightness mode
  if (brightness == Brightness.light) {
    // Light mode
    setState(() {
      // Update UI components for light mode
    });
  } else {
    // Dark mode
    setState(() {
      // Update UI components for dark mode
    });
  }
}
```

## Step 5: Implement the UIChangeListener in your app

In your app's main widget, use the `UIChangeListener` widget to wrap the widget tree. This will allow the app to listen for system UI mode changes and update the UI accordingly:

```dart
void main() {
  runApp(MaterialApp(
    home: UIChangeListener(
      child: YourAppWidget(),
    ),
  ));
}
```

Make sure to replace `YourAppWidget` with the root widget of your app.

## Conclusion

In this blog post, we have seen how to listen for system UI mode changes using `MediaQuery` in Flutter. By overriding the `didChangeMetrics` method and using `MediaQuery.of(context).platformBrightness`, we can detect changes in the system UI mode and update the UI accordingly.

Remember to test your app on devices with different UI modes to ensure that the UI updates correctly. Happy Flutter coding!

\#Flutter #SystemUIModeChanges