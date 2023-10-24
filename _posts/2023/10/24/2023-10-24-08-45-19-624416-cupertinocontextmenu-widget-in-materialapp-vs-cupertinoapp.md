---
layout: post
title: "CupertinoContextMenu widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When creating a mobile app using Flutter and you want to incorporate a context menu, you have two options - using CupertinoContextMenu widget within MaterialApp or within CupertinoApp.

The CupertinoContextMenu widget provides a contextual menu that can be triggered by a long press on a specific widget. It is designed to adhere to the iOS design guidelines, providing a native iOS look and feel. 

Let's compare the usage of CupertinoContextMenu widget in MaterialApp and CupertinoApp:

## 1. CupertinoContextMenu in MaterialApp

### Code example:
```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      appBar: AppBar(
        title: Text('CupertinoContextMenu in MaterialApp'),
      ),
      body: Center(
        child: CupertinoContextMenu(
          actions: <Widget>[
            CupertinoContextMenuAction(
              child: Text('Option 1'),
              onPressed: () {
                // Action when Option 1 is pressed
              },
            ),
            CupertinoContextMenuAction(
              child: Text('Option 2'),
              onPressed: () {
                // Action when Option 2 is pressed
              },
            ),
          ],
          child: Container(
            height: 200,
            width: 200,
            color: Colors.blue,
            child: Center(
              child: Text(
                'Long press to open context menu',
                style: TextStyle(color: Colors.white),
              ),
            ),
          ),
        ),
      ),
    ),
  ));
}
```

In MaterialApp, you can use the CupertinoContextMenu widget just like any other widget. It can be placed within the widget tree wherever needed. You need to wrap the widget that you want to use as the trigger for the context menu in the CupertinoContextMenu widget. 

## 2. CupertinoContextMenu in CupertinoApp

### Code example:
```dart
import 'package:flutter/cupertino.dart';

void main() {
  runApp(CupertinoApp(
    home: CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(
        middle: Text('CupertinoContextMenu in CupertinoApp'),
      ),
      child: Center(
        child: CupertinoContextMenu(
          actions: <Widget>[
            CupertinoContextMenuAction(
              child: Text('Option 1'),
              onPressed: () {
                // Action when Option 1 is pressed
              },
            ),
            CupertinoContextMenuAction(
              child: Text('Option 2'),
              onPressed: () {
                // Action when Option 2 is pressed
              },
            ),
          ],
          child: Container(
            height: 200,
            width: 200,
            color: Colors.blue,
            child: Center(
              child: Text(
                'Long press to open context menu',
                style: TextStyle(color: Colors.white),
              ),
            ),
          ),
        ),
      ),
    ),
  ));
}
```

In CupertinoApp, you wrap the CupertinoContextMenu widget around the widget you want to serve as the context menu trigger. CupertinoApp is more suitable if you are targeting an iOS-specific app and want to maintain consistency with iOS design guidelines.

## Conclusion

Whether you choose to use CupertinoContextMenu in MaterialApp or CupertinoApp depends on the specific needs of your app. MaterialApp allows for cross-platform compatibility, while CupertinoApp provides a more iOS-specific look and feel. Consider your app's target platform and design requirements when making the choice.

# References

- [CupertinoContextMenu widget documentation](https://api.flutter.dev/flutter/cupertino/CupertinoContextMenu-class.html)
- [Flutter Cupertino widgets](https://api.flutter.dev/flutter/cupertino/cupertino-library.html)