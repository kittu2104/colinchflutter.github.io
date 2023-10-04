---
layout: post
title: "useSelectableText hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: [flutterhooks]
comments: true
share: true
---

Flutter Hooks is a popular package that provides a set of hooks to enhance the functionality of Flutter widgets. One of these hooks is `useSelectableText`, which allows you to make text selectable in your Flutter application. In this article, we will explore how to use the `useSelectableText` hook and demonstrate its functionality with an example.

## Installation

Before we can start using Flutter Hooks and the `useSelectableText` hook, make sure that you have the `flutter_hooks` package added as a dependency in your `pubspec.yaml` file. You can install it by running the following command in your terminal:

```dart
dependencies:
  flutter_hooks: ^0.18.0
```

After adding the dependency, run `flutter pub get` to fetch the package.

## Usage

To use the `useSelectableText` hook, import it from the `flutter_hooks` package as follows:

```dart
import 'package:flutter_hooks/flutter_hooks.dart';
```

Now, let's proceed to see how we can use the `useSelectableText` hook. For this example, we will create a simple Flutter application that displays selectable text when tapped.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_hooks/flutter_hooks.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends HookWidget {
  @override
  Widget build(BuildContext context) {
    final textController = useSelectableTextController();

    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Selectable Text Example'),
        ),
        body: Center(
          child: GestureDetector(
            onTap: () {
              textController.selectText();
            },
            child: useSelectableText(
              text: 'Tap to select this text',
              controller: textController,
              style: TextStyle(fontSize: 18),
            ),
          ),
        ),
      ),
    );
  }
}
```

In the above code, we have created a simple Flutter application with `MyApp` as the root widget. Inside the `build` method of `MyApp`, we define a `textController` using the `useSelectableTextController` hook. This controller is responsible for managing the state of the selectable text.

Next, we use the `useSelectableText` hook to create a selectable text widget. We pass the `text` parameter with the desired text to be displayed, `controller` with the text controller, and `style` to define the text style. By wrapping the `useSelectableText` widget with a `GestureDetector`, we make the text selectable when tapped.

## Conclusion

In this article, we learned about the `useSelectableText` hook provided by the Flutter Hooks package. We explored how to use it to create selectable text in a Flutter application and demonstrated its usage with an example. Feel free to experiment with the `useSelectableText` hook and explore its capabilities further in your own projects.

#flutter #flutterhooks