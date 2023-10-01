---
layout: post
title: "useClipRRect hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: [Flutter, FlutterHooks]
comments: true
share: true
---

Flutter Hooks is a package that provides a set of utility hooks to build Flutter applications. One of the hooks provided by Flutter Hooks is `useClipRRect`, which allows you to easily apply a rounded rectangle clip to a widget.

## Installation

To use Flutter Hooks and the `useClipRRect` hook, you need to add the following dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_hooks: ^0.20.0
```

After adding the dependency, run `flutter pub get` to fetch the package.

## Usage

Here's an example of how to use the `useClipRRect` hook in your Flutter application:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_hooks/flutter_hooks.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends HookWidget {
  @override
  Widget build(BuildContext context) {
    final borderRadius = useState(10.0);

    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('ClipRRect Hook Example'),
        ),
        body: Center(
          child: ClipRRect(
            borderRadius: BorderRadius.circular(borderRadius.value),
            child: Container(
              width: 200,
              height: 200,
              color: Colors.blue,
              child: Text(
                'Hello Flutter Hooks',
                style: TextStyle(fontSize: 24, color: Colors.white),
              ),
            ),
          ),
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: () {
            borderRadius.value = borderRadius.value == 10.0 ? 50.0 : 10.0;
          },
          child: Icon(Icons.rounded_corner),
        ),
      ),
    );
  }
}
```

In the example above, we define a function component called `MyApp` that uses the `HookWidget` class from the `flutter_hooks` package. Within `MyApp`, we create a state variable called `borderRadius` using the `useState` hook, which allows us to dynamically change the corner radius of the `ClipRRect` widget.

Inside the `ClipRRect` widget, we apply the `borderRadius` value to the `borderRadius` property of the `BorderRadius.circular` object. This allows us to change the corner radius of the rectangle based on the value of `borderRadius`.

The `floatingActionButton` is used to toggle between a rounded corner and a square corner. When pressed, it updates the `borderRadius` value to either `10.0` or `50.0`.

## Conclusion

With the `useClipRRect` hook provided by Flutter Hooks, applying a rounded rectangle clip to a widget has never been easier. You can dynamically change the corner radius and create visually appealing user interfaces with rounded corners in your Flutter applications.

#Flutter #FlutterHooks