---
layout: post
title: "Dialog boxes in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

Both `MaterialApp` and `CupertinoApp` are popular choices when developing mobile applications using Flutter. These two classes provide different sets of UI components, including dialog boxes. Let's compare how dialog boxes are implemented in these two frameworks.

## Dialog boxes in MaterialApp

In `MaterialApp`, dialog boxes are based on the Material Design style. Flutter provides a predefined `showDialog` method that can be used to display a dialog box to the user.

Here is an example of how to use `showDialog` in a `MaterialApp`:

```dart
RaisedButton(
  onPressed: () {
    showDialog(
      context: context,
      builder: (BuildContext context) {
        return AlertDialog(
          title: Text('Dialog Box'),
          content: Text('This is a dialog box.'),
          actions: [
            FlatButton(
              child: Text('Close'),
              onPressed: () {
                Navigator.of(context).pop();
              },
            ),
          ],
        );
      },
    );
  },
  child: Text('Open Dialog'),
)
```

In the above code, we create a `RaisedButton` that opens a dialog box when pressed. Inside the `showDialog` method, we provide a context and a builder function that returns the content of the dialog box.

## Dialog boxes in CupertinoApp

In `CupertinoApp`, dialog boxes are based on the iOS design style. Flutter provides the `showDialog` method as well, but it uses a different implementation to match the CupertinoDesign.

Here is an example of how to use `showDialog` in a `CupertinoApp`:

```dart
FlatButton(
  onPressed: () {
    showCupertinoDialog(
      context: context,
      builder: (BuildContext context) {
        return CupertinoAlertDialog(
          title: Text('Dialog Box'),
          content: Text('This is a dialog box.'),
          actions: [
            FlatButton(
              child: Text('Close'),
              onPressed: () {
                Navigator.of(context).pop();
              },
            ),
          ],
        );
      },
    );
  },
  child: Text('Open Dialog'),
)
```

In the above code, we use `showCupertinoDialog` instead of `showDialog` to open a Cupertino-style dialog box. Similar to the `MaterialApp` example, we provide a context and a builder function that returns the content of the dialog box.

## Conclusion

Both `MaterialApp` and `CupertinoApp` provide convenient ways to display dialog boxes in Flutter applications. The choice between them depends on the desired style and design guidelines you want to follow. Choose `MaterialApp` for Material Design or `CupertinoApp` for iOS-like design.