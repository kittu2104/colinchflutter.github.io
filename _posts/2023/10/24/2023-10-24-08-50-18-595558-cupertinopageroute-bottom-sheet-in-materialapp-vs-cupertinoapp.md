---
layout: post
title: "CupertinoPageRoute bottom sheet in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When building a cross-platform app, you might come across scenarios where you need to create a bottom sheet in your user interface. In Flutter, you have the option to use either `MaterialApp` or `CupertinoApp` as the base widget for your app. Each offers its own set of UI components and design language.

## Using Bottom Sheet with MaterialApp

If you choose to use `MaterialApp` as the foundation for your app, you have access to the widely-used Material Design components. To create a bottom sheet, you can use the `showModalBottomSheet` method provided by the Scaffold widget.

Here's an example code snippet that demonstrates how to create a bottom sheet using MaterialApp:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      appBar: AppBar(
        title: Text('Material Bottom Sheet'),
      ),
      body: Center(
        child: ElevatedButton(
          child: Text('Open Bottom Sheet'),
          onPressed: () {
            showModalBottomSheet(
              context: context,
              builder: (BuildContext context) {
                return Container(
                  // Bottom sheet content
                );
              },
            );
          },
        ),
      ),
    ),
  ));
}
```

## Using Bottom Sheet with CupertinoApp

On the other hand, if you prefer to utilize the iOS design style provided by Cupertino, you can use the `CupertinoApp` widget as your app's base. Cupertino offers its own set of UI components, including its own version of a bottom sheet.

To create a bottom sheet using `CupertinoApp`, you can use the `showCupertinoModalPopup` method provided by the Cupertino widget library.

Here's an example code snippet that demonstrates how to create a bottom sheet using CupertinoApp:

```dart
import 'package:flutter/cupertino.dart';

void main() {
  runApp(CupertinoApp(
    home: CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(
        middle: Text('Cupertino Bottom Sheet'),
      ),
      child: Center(
        child: CupertinoButton(
          child: Text('Open Bottom Sheet'),
          onPressed: () {
            showCupertinoModalPopup(
              context: context,
              builder: (BuildContext context) {
                return Container(
                  // Bottom sheet content
                );
              },
            );
          },
        ),
      ),
    ),
  ));
}
```

## Key Differences

When comparing the bottom sheets in `MaterialApp` and `CupertinoApp`, there are a few key differences to note:

- **Visual Style:** The bottom sheet in `MaterialApp` adheres to the Material Design language and looks more like a card. In contrast, the bottom sheet in `CupertinoApp` follows the iOS design language with a semi-transparent look.

- **Animations:** The animation used to show and hide the bottom sheet differs between the two. The Material bottom sheet slides up from the bottom, while the Cupertino bottom sheet appears to be pushed up from the bottom.

- **Usage:** If you are developing a cross-platform app and want to maintain a consistent design language across both iOS and Android, using `MaterialApp` and the Material bottom sheet may be the way to go. However, if you are specifically targeting iOS devices and want to provide a native user experience, `CupertinoApp` and the Cupertino bottom sheet will be more suitable.

Regardless of the approach you choose, both `MaterialApp` and `CupertinoApp` provide convenient ways to implement bottom sheets in your Flutter app. Consider the design language and target platform when deciding which one to use.