---
layout: post
title: "Cupertino dialog customization in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [tags]
comments: true
share: true
---

When it comes to Flutter app development, you have the option to choose between `MaterialApp` and `CupertinoApp` as the base widget for your application. Both provide different design styles and UI components, including the `CupertinoDialog`, which is a pre-styled dialog component in iOS.

However, the customization options for the `CupertinoDialog` differ slightly between the two base widgets. Let's take a closer look at customizing the Cupertino dialog in each.

## Customization in MaterialApp

When using the `MaterialApp` widget as the base for your Flutter app, you can still display a Cupertino-style dialog by using the `CupertinoDialog` class. However, to fully customize the appearance of the dialog, you would need to override the entire dialog widget or use a package that provides custom dialogs for `MaterialApp`.

There are several packages available that offer customized iOS-style dialogs for Flutter, such as the `flutter_cupertino_dialog` package. These packages provide various customization options, including changing the dialog title, content, button colors, and more.

Here's an example of how you can use the `flutter_cupertino_dialog` package to customize a Cupertino-style dialog within a `MaterialApp`:

```dart
import 'package:flutter_cupertino_dialog/flutter_cupertino_dialog.dart';

showCupertinoDialog(
  context: context,
  builder: (BuildContext context) => CupertinoAlertDialog(
    title: Text('Custom Dialog Title'),
    content: Text('Custom Dialog Content'),
    actions: <Widget>[
      CupertinoDialogAction(
        child: Text('Cancel'),
        onPressed: () => Navigator.pop(context),
      ),
      CupertinoDialogAction(
        child: Text('Confirm'),
        onPressed: () {
          // Add your confirm logic here
        },
      ),
    ],
  ),
);
```

## Customization in CupertinoApp

If you choose to use the `CupertinoApp` widget as the base for your Flutter app, you can directly customize the default appearance of the `CupertinoDialog` using the available properties and widgets.

The `CupertinoDialog` class provides properties such as `title`, `content`, `actions`, and `backgroundColor` that can be used to customize the dialog's appearance.

Here's an example of how you can customize a Cupertino-style dialog directly within a `CupertinoApp`:

```dart
CupertinoDialog(
  title: Text('Custom Dialog Title'),
  content: Text('Custom Dialog Content'),
  actions: <Widget>[
    CupertinoDialogAction(
      child: Text('Cancel'),
      onPressed: () => Navigator.pop(context),
    ),
    CupertinoDialogAction(
      child: Text('Confirm'),
      onPressed: () {
        // Add your confirm logic here
      },
    ),
  ],
)
```

By leveraging the properties of the `CupertinoDialog`, you can easily customize the look and feel of the dialog within the `CupertinoApp` widget.

# Conclusion

Both `MaterialApp` and `CupertinoApp` offer different customization options for the `CupertinoDialog` in Flutter. While the `MaterialApp` requires additional packages for full customization, the `CupertinoApp` allows direct customization using the available properties of the `CupertinoDialog` class. Choose the widget that suits your app's design and customization requirements.

# References
- Flutter Cupertino dialog package: [flutter_cupertino_dialog](https://pub.dev/packages/flutter_cupertino_dialog)
- Flutter CupertinoApp documentation: [CupertinoApp class](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html)
- Flutter MaterialApp documentation: [MaterialApp class](https://api.flutter.dev/flutter/material/MaterialApp-class.html)

#tags: flutter, cupertino, material, customization, dialog