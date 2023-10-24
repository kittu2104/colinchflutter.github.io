---
layout: post
title: "CupertinoPageRoute fullscreen dialogs in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [references]
comments: true
share: true
---

When developing a mobile app using Flutter, you have the option to choose between `MaterialApp` and `CupertinoApp` as the base widget for your app. Both provide different visual styles and UI conventions, with `MaterialApp` following the Material Design guidelines and `CupertinoApp` following the iOS design principles.

One area where the difference between the two becomes prominent is when working with fullscreen dialogs using `CupertinoPageRoute`. Let's explore how these fullscreen dialogs behave in `MaterialApp` and `CupertinoApp`.

## Fullscreen Dialogs in MaterialApp

When using `MaterialApp`, fullscreen dialogs are presented with a background scrim behind them. This scrim darkens the background content and adds a layer of focus to the dialog. The dialog itself is centered on the screen and occupies the entire available space, giving it a truly fullscreen experience.

To create a fullscreen dialog in `MaterialApp`, you can use the `showDialog` method along with `MaterialPageRoute`. Here's an example:

```dart
showDialog(
  context: context,
  builder: (BuildContext context) {
    return Dialog(
      child: Container(
        height: MediaQuery.of(context).size.height,
        width: MediaQuery.of(context).size.width,
        child: Center(
          child: Text('Fullscreen Dialog'),
        ),
      ),
    );
  },
);
```

## Fullscreen Dialogs in CupertinoApp

On the other hand, when using `CupertinoApp`, fullscreen dialogs are presented without the background scrim or darkening effect found in `MaterialApp`. Instead, the dialog is shown as a standalone card-like component, still centered on the screen but without the extra visual layer behind it.

To create a fullscreen dialog in `CupertinoApp`, you can use the `showDialog` method along with `CupertinoPageRoute`. Here's an example:

```dart
showDialog(
  context: context,
  builder: (BuildContext context) {
    return CupertinoAlertDialog(
      title: Text('Fullscreen Dialog'),
      content: Text('This is a fullscreen dialog.'),
      actions: [
        CupertinoDialogAction(
          child: Text('Close'),
          onPressed: () => Navigator.of(context).pop(),
        ),
      ],
    );
  },
);
```

## Conclusion

The choice between `MaterialApp` and `CupertinoApp` depends on the desired visual style and UI conventions for your app. When it comes to fullscreen dialogs, `MaterialApp` provides a more visually prominent experience with the scrim background, while `CupertinoApp` presents dialogs in a cleaner, more minimalistic way.

Remember to consider your target platform and design guidelines when deciding which base widget to use, as it can significantly impact the overall look and feel of your app.

#references
- [CupertinoPageRoute class documentation](https://api.flutter.dev/flutter/cupertino/CupertinoPageRoute-class.html)
- [MaterialPageRoute class documentation](https://api.flutter.dev/flutter/material/MaterialPageRoute-class.html)