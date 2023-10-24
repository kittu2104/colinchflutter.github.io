---
layout: post
title: "Cupertino progress indicator customization in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [References]
comments: true
share: true
---

When developing mobile applications with Flutter, you can choose between two main frameworks: `MaterialApp` and `CupertinoApp`. `MaterialApp` is based on the Material Design language by Google, while `CupertinoApp` follows the design principles of Apple's iOS.

One of the key components in a mobile application is the progress indicator, which notifies the user about ongoing tasks or loading processes. Flutter provides both Material and Cupertino versions of progress indicators. Let's explore how to customize the Cupertino progress indicator in both `MaterialApp` and `CupertinoApp`.

## Customizing Cupertino Progress Indicator in MaterialApp

In a Flutter application using `MaterialApp`, you can customize the Cupertino progress indicator by modifying the `ThemeData` for `ThemeData.cupertinoOverrideTheme`.

1. Start by importing the required packages:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/cupertino.dart';
```

2. Create a `MaterialApp` widget and define a `ThemeData` object:

```dart
void main() {
  runApp(MaterialApp(
    theme: ThemeData(
      cupertinoOverrideTheme: CupertinoThemeData(
        // Customization options go here
      ),
    ),
    home: MyApp(),
  ));
}
```

3. Customize the `CupertinoThemeData` in the `cupertinoOverrideTheme` by specifying properties such as `primaryColor`, `accentColor`, or `brightness`.

## Customizing Cupertino Progress Indicator in CupertinoApp

Meanwhile, if your application uses the `CupertinoApp` framework, you can customize the Cupertino progress indicator by directly modifying the `CupertinoThemeData` within the `CupertinoApp` widget.

1. Import the required packages:

```dart
import 'package:flutter/cupertino.dart';
```

2. Create a `CupertinoApp` widget and define the `CupertinoThemeData`:

```dart
void main() {
  runApp(CupertinoApp(
    theme: CupertinoThemeData(
      // Customization options go here
    ),
    home: MyApp(),
  ));
}
```

3. Customize the `CupertinoThemeData` by specifying properties such as `primaryColor`, `textTheme`, or `barBackgroundColor`.

## Conclusion

Customizing the Cupertino progress indicator in both `MaterialApp` and `CupertinoApp` involves modifying the relevant theme data. With `MaterialApp`, you can modify the `cupertinoOverrideTheme` within the overall `ThemeData`. On the other hand, in `CupertinoApp`, you directly modify the `CupertinoThemeData` within the `CupertinoApp` widget.

By customizing the progress indicator, you can enhance the user experience and ensure it aligns with the design and branding of your application.

#References
- Flutter documentation: [MaterialApp](https://api.flutter.dev/flutter/material/MaterialApp-class.html)
- Flutter documentation: [CupertinoApp](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html)
- Flutter documentation: [CupertinoThemeData](https://api.flutter.dev/flutter/cupertino/CupertinoThemeData-class.html)