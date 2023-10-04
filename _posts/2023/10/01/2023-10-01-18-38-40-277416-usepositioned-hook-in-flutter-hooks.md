---
layout: post
title: "usePositioned hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: [FlutterHooks]
comments: true
share: true
---

Flutter Hooks is a powerful package that allows developers to build Flutter applications using modern hooks-based programming techniques. One handy hook provided by Flutter Hooks is `usePositioned`, which helps in positioning widgets within a `Stack`.

## Understanding `usePositioned`

The `usePositioned` hook is similar to Flutter's `Positioned` widget. It allows you to specify the position of a child widget within a `Stack` by using absolute coordinates. The `usePositioned` hook returns a `Positioned` widget that you can use in your Flutter UI.

## Installation

To use the `usePositioned` hook, you'll need to have the Flutter Hooks package added as a dependency in your `pubspec.yaml` file. You can do this by adding the following line under the `dependencies` section:

```yaml
dependencies:
  flutter_hooks: ^0.18.0
```

After adding the dependency, run `flutter pub get` in your terminal to fetch and install the package.

## Usage

Here's an example of how you can use the `usePositioned` hook in a Flutter application:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_hooks/flutter_hooks.dart';

class PositionedDemo extends HookWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Positioned Demo'),
      ),
      body: Center(
        child: Stack(
          children: [
            Container(
              width: 200,
              height: 200,
              color: Colors.green,
            ),
            usePositioned(
              left: 50,
              top: 50,
              child: Container(
                width: 100,
                height: 100,
                color: Colors.red,
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

In this example, we import the `flutter_hooks` package and create a `HookWidget` called `PositionedDemo`. Inside the `build` method, we use a `Stack` widget to stack two `Container` widgets. 

The first `Container` is just a green square that acts as the base. We then use the `usePositioned` hook to position the second `Container` widget at the top left corner of the `Stack`. By specifying `left: 50` and `top: 50`, we offset the widget by 50 pixels from the top and left edges of the `Stack`, creating a red square in the top left corner.

You can modify the position properties (`left`, `top`, `right`, `bottom`) and other parameters of `usePositioned` to achieve the desired positioning of your widgets.

## Conclusion

The `usePositioned` hook from Flutter Hooks provides a convenient way to position widgets within a `Stack` using absolute coordinates. By utilizing this hook, you can easily create complex UI layouts in your Flutter applications. Give it a try and enhance your app's user experience by mastering the power of hooks-based programming with Flutter Hooks.

#flutter #FlutterHooks