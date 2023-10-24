---
layout: post
title: "CupertinoActivityIndicator widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

In Flutter, the `CupertinoActivityIndicator` widget is used to display an iOS-style activity indicator, which spins in a circular motion to indicate that something is happening in the background.

When using this widget, you have the flexibility to choose between two main application classes: `MaterialApp` and `CupertinoApp`. Each has its own set of specific features and design guidelines.

Let's explore the differences and use cases for `CupertinoActivityIndicator` in both `MaterialApp` and `CupertinoApp`.

## MaterialApp

`MaterialApp` is the widget class used to implement Material Design guidelines in your Flutter app. It provides a visually appealing and consistent UI on both Android and iOS platforms.

To use `CupertinoActivityIndicator` in `MaterialApp`, you need to import the `cupertino_icons` package in your `pubspec.yaml` file and ensure that you have it available in your project.

```dart
dependencies:
  flutter:
    sdk: flutter
  cupertino_icons: ^1.0.4
```

Next, you can use the `CupertinoActivityIndicator` widget within a `CircularProgressIndicator` and wrap it with a `Center` widget to center it on the screen.

```dart
import 'package:flutter/material.dart';
import 'package:flutter/cupertino.dart';

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      appBar: AppBar(
        title: Text('Material App with CupertinoActivityIndicator'),
      ),
      body: Center(
        child: CircularProgressIndicator(
          valueColor: AlwaysStoppedAnimation<Color>(Colors.blue),
          strokeWidth: 4.0,
        ),
      ),
    ),
  ));
}
```

## CupertinoApp

`CupertinoApp` is the widget class used to implement Cupertino Design guidelines in your Flutter app. It provides an iOS-like UI experience with familiar iOS widgets.

To use `CupertinoActivityIndicator` in `CupertinoApp`, you don't need to import the `cupertino_icons` package explicitly since it is already bundled with the `cupertino` package.

You can use the `CupertinoActivityIndicator` widget directly within a `Center` widget to achieve a centered activity indicator.

```dart
import 'package:flutter/cupertino.dart';

void main() {
  runApp(CupertinoApp(
    home: CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(
        middle: Text('Cupertino App with CupertinoActivityIndicator'),
      ),
      child: Center(
        child: CupertinoActivityIndicator(
          radius: 20.0,
        ),
      ),
    ),
  ));
}
```

## Conclusion

The choice between `MaterialApp` and `CupertinoApp` depends on whether you want to follow Material Design or Cupertino Design guidelines for your app's UI. When using `MaterialApp`, you need to import the `cupertino_icons` package explicitly, whereas `CupertinoApp` comes with Cupertino-specific icons bundled in the `cupertino` package. Whichever app class you choose, `CupertinoActivityIndicator` will work similarly to show a spinning activity indicator.

Remember to import the necessary packages and wrap the `CupertinoActivityIndicator` widget with appropriate parent widgets like `Scaffold` and `Center` for `MaterialApp`, and `CupertinoPageScaffold` and `Center` for `CupertinoApp`.

Most importantly, don't forget to experiment with different customization options available for `CupertinoActivityIndicator` to match your app's design and aesthetics.

For more details, you can refer to the official Flutter documentation on [CupertinoActivityIndicator](https://api.flutter.dev/flutter/cupertino/CupertinoActivityIndicator-class.html), [MaterialApp](https://api.flutter.dev/flutter/material/MaterialApp-class.html), and [CupertinoApp](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html).

#flutter #flutterdesign