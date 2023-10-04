---
layout: post
title: "MediaQuery disableAnimations in Flutter"
description: " "
date: 2023-10-01
tags: [Animations]
comments: true
share: true
---

Animations are an integral part of creating engaging user experiences in Flutter apps. However, sometimes you may need to disable animations for various reasons, such as during testing or to accommodate users with motion sensitivities. In Flutter, you can easily disable animations using the `MediaQuery` class. In this article, we'll discuss how to disable animations in Flutter using `MediaQuery`.

## What is MediaQuery?

`MediaQuery` is a Flutter class that provides access to various information about the user's device, such as screen size, orientation, text scale factor, and more. It acts as a conduit between your app and the underlying platform, allowing you to customize your app's behavior based on the device's characteristics.

## Disabling Animations using MediaQuery

To disable animations in Flutter, we can utilize the `disableAnimations` property of the `MediaQueryData` class. `disableAnimations` is a boolean value that, when set to `true`, disables all animations in the app.

Let's see an example of how to disable animations using `MediaQuery` in Flutter:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: MediaQuery(
        data: MediaQuery.of(context).copyWith(
          disableAnimations: true,
        ),
        child: MyHomePage(),
      ),
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Disable Animations'),
      ),
      body: Center(
        child: Text(
          'Animations Disabled',
          style: TextStyle(
            fontSize: 24.0,
            fontWeight: FontWeight.bold,
          ),
        ),
      ),
    );
  }
}
```

In the example above, we wrap the `MyHomePage` widget with a `MediaQuery` widget and set the `disableAnimations` property to `true` using `MediaQuery.of(context).copyWith()`. This ensures that all animations within the `MediaQuery` context are disabled.

## Summary

Disabling animations in Flutter using `MediaQuery` is a straightforward process. By setting the `disableAnimations` property to `true`, you can easily disable animations in your app. Remember to use this feature responsibly and consider the impact on the overall user experience.

#Flutter #Animations