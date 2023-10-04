---
layout: post
title: "How to get the device's platform brightness using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [brightness]
comments: true
share: true
---

When developing a Flutter app, it's important to be able to adjust the screen brightness based on the device's platform brightness settings. This ensures a consistent user experience across different devices and operating systems. In Flutter, you can easily retrieve the device's platform brightness using the `MediaQuery` class. Let's dive into the code!

## Step 1: Import the required packages

First, you need to import the necessary packages in your Dart file:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';
```

## Step 2: Retrieve the platform brightness

To retrieve the device's platform brightness, you can use the `brightness` property of the `MediaQueryData` class. The `MediaQueryData` class provides information about the current media, such as the size and orientation of the screen.

```dart
Brightness brightness = MediaQuery.of(context).platformBrightness;
```

The `brightness` variable will now hold the value of the platform brightness. You can use this value to adjust the brightness of your app's UI elements accordingly.

## Step 3: Adjust the UI based on brightness

You can now use the `brightness` variable to adjust the UI elements in your app. For example, you might want to change the color of a `Text` widget based on the brightness setting. Here's an example:

```dart
Color textColor = brightness == Brightness.dark ? Colors.white : Colors.black;

Text(
  'Hello, World!',
  style: TextStyle(
    color: textColor,
  ),
);
```

In this example, if the platform brightness is set to dark, the `Text` widget will have white text color. Otherwise, it will have black text color. You can use this approach to adapt various UI elements in your app based on the device's platform brightness.

That's it! By using `MediaQuery` in Flutter, you can easily retrieve the device's platform brightness and adjust your app's UI elements accordingly. This ensures a consistent and user-friendly experience for your users.

#flutter #brightness