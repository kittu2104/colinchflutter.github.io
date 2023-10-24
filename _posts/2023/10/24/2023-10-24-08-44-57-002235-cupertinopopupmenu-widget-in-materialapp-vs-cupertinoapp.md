---
layout: post
title: "CupertinoPopupMenu widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

In Flutter, the `CupertinoPopupMenu` widget is used to create a popup menu that follows the iOS design guidelines. It provides a menu that appears when the user taps on a button or any other widget.

There are two main ways to use the `CupertinoPopupMenu` widget: within a `MaterialApp` or within a `CupertinoApp`. Let's explore the differences between the two approaches.

## 1. CupertinoPopupMenu in MaterialApp

When using the `CupertinoPopupMenu` widget within a `MaterialApp`, the appearance of the popup menu will follow the Material Design guidelines. It will have a slightly different look and feel compared to iOS-style popup menus.

To create a Cupertino-style popup menu in a `MaterialApp`, you can use the `CupertinoPopupSurface` widget as the child of a `PopupMenuItem`. This way, you can maintain an iOS style while still working within the Material design system.

Here's an example of how to use `CupertinoPopupSurface` in the context of a `MaterialApp`:

```dart
MaterialApp(
  home: Scaffold(
    appBar: AppBar(
      title: Text('Example'),
    ),
    body: Center(
      child: PopupMenuButton(
        itemBuilder: (BuildContext context) {
          return <PopupMenuEntry>[
            PopupMenuItem(
              child: CupertinoPopupSurface(
                child: Text('Option 1'),
              ),
            ),
            PopupMenuItem(
              child: CupertinoPopupSurface(
                child: Text('Option 2'),
              ),
            ),
            PopupMenuItem(
              child: CupertinoPopupSurface(
                child: Text('Option 3'),
              ),
            ),
          ];
        },
      ),
    ),
  ),
);
```

## 2. CupertinoPopupMenu in CupertinoApp

If you want the `CupertinoPopupMenu` to have the native iOS look and feel, you should use it within a `CupertinoApp`. This will ensure that the popup menu adheres to the design guidelines of iOS.

To use it, you can simply wrap your widget tree within a `CupertinoApp` and include the `CupertinoPopupMenu` widget as needed.

Here's an example of how to use `CupertinoPopupMenu` within a `CupertinoApp`:

```dart
CupertinoApp(
  home: CupertinoPageScaffold(
    navigationBar: CupertinoNavigationBar(
      middle: Text('Example'),
    ),
    child: Center(
      child: CupertinoButton(
        child: Text('Show Menu'),
        onPressed: () {
          showCupertinoModalPopup(
            context: context,
            builder: (BuildContext context) => CupertinoActionSheet(
              cancelButton: CupertinoButton(
                child: Text('Cancel'),
                onPressed: () {
                  Navigator.of(context).pop();
                },
              ),
              actions: <Widget>[
                CupertinoActionSheetAction(
                  child: Text('Option 1'),
                  onPressed: () {
                    Navigator.of(context).pop();
                    // perform action
                  },
                ),
                CupertinoActionSheetAction(
                  child: Text('Option 2'),
                  onPressed: () {
                    Navigator.of(context).pop();
                    // perform action
                  },
                ),
                CupertinoActionSheetAction(
                  child: Text('Option 3'),
                  onPressed: () {
                    Navigator.of(context).pop();
                    // perform action
                  },
                ),
              ],
            ),
          );
        },
      ),
    ),
  ),
);
```

In the above example, we wrap our app's navigation bar and content area within a `CupertinoPageScaffold`. The `CupertinoActionSheet` widget is used to create the popup menu.

## Conclusion

In summary, when using `CupertinoPopupMenu` within a `MaterialApp`, the appearance of the menu will follow Material Design guidelines, while using it within a `CupertinoApp` will give it a native iOS look and feel. Choose the approach that best suits the overall design and platform consistency of your Flutter application.

# References
- [CupertinoPopupMenu class - Flutter API documentation](https://api.flutter.dev/flutter/cupertino/CupertinoPopupMenu-class.html)
- [Understanding the Cupertino design language - Flutter.dev](https://flutter.dev/docs/development/ui/widgets/cupertino)