---
layout: post
title: "CupertinoAlertDialog widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [dialog]
comments: true
share: true
---

In Flutter, there are two main ways to create alerts or dialogs in your app: using the `CupertinoAlertDialog` widget inside a `MaterialApp` or using it inside a `CupertinoApp`. While both approaches can achieve the same result, there are some notable differences between the two.

## Using CupertinoAlertDialog in MaterialApp

The `MaterialApp` is the default app structure in Flutter and provides a Material Design layout for your app. When you use the `CupertinoAlertDialog` widget within a `MaterialApp`, Flutter will automatically adapt the design to match the Material Design guidelines. This means that the alert dialog will have a visually different look and feel compared to alerts in the iOS style.

Here's an example of how to use `CupertinoAlertDialog` within a `MaterialApp`:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/cupertino.dart';

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      appBar: AppBar(
        title: Text('Alert Example'),
      ),
      body: Center(
        child: ElevatedButton(
          child: Text('Show Alert'),
          onPressed: () {
            showDialog(
              context: context,
              builder: (BuildContext context) {
                return CupertinoAlertDialog(
                  title: Text('Alert'),
                  content: Text('This is an alert dialog.'),
                  actions: [
                    CupertinoDialogAction(
                      child: Text('OK'),
                      onPressed: () {
                        Navigator.of(context).pop();
                      },
                    ),
                  ],
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

## Using CupertinoAlertDialog in CupertinoApp

On the other hand, the `CupertinoApp` provides an iOS-style app structure. When using the `CupertinoAlertDialog` widget inside a `CupertinoApp`, Flutter will ensure that the alert dialog follows the iOS design guidelines, giving it a visually distinct appearance.

To use `CupertinoAlertDialog` within a `CupertinoApp`, you can modify the previous example as follows:

```dart
import 'package:flutter/cupertino.dart';

void main() {
  runApp(CupertinoApp(
    home: CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(
        middle: Text('Alert Example'),
      ),
      child: Center(
        child: CupertinoButton(
          child: Text('Show Alert'),
          onPressed: () {
            showCupertinoDialog(
              context: context,
              builder: (BuildContext context) {
                return CupertinoAlertDialog(
                  title: Text('Alert'),
                  content: Text('This is an alert dialog.'),
                  actions: [
                    CupertinoDialogAction(
                      child: Text('OK'),
                      onPressed: () {
                        Navigator.of(context).pop();
                      },
                    ),
                  ],
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

## Conclusion

When using the `CupertinoAlertDialog` widget in Flutter, you can choose between using it in a `MaterialApp` or a `CupertinoApp`. Depending on the app's design and targeted platform, you can select the appropriate app structure to ensure consistent visual appearance of your alert dialogs. Keep in mind that using `CupertinoApp` provides an iOS-style look, while using `MaterialApp` results in a Material Design-style alert dialog.

#flutter #dialog