---
layout: post
title: "CupertinoPageRoute dismissible modal in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

In Flutter, there are two ways to create dismissible modals using the CupertinoPageRoute: 

1. **Using MaterialApp**: If you are using the MaterialApp widget as the root of your app, you can create a dismissible modal using the MaterialPageRoute. 

```dart
Navigator.of(context).push(
  MaterialPageRoute(
    builder: (BuildContext context) {
      return YourModalWidget();
    },
    fullscreenDialog: true,
  ),
);
```

Notice the `fullscreenDialog` property set to `true`. This ensures that the modal is displayed as a fullscreen dialog and provides a built-in dismiss gesture.

2. **Using CupertinoApp**: If you are using the CupertinoApp widget as the root of your app, you can create a dismissible modal using the CupertinoPageRoute.

```dart
Navigator.of(context).push(
  CupertinoPageRoute(
    builder: (BuildContext context) {
      return YourModalWidget();
    },
    fullscreenDialog: true,
  ),
);
```

The usage of CupertinoPageRoute is similar to the one in MaterialApp. Set the `fullscreenDialog` property to `true` to display the modal as a fullscreen dialog.

## The Difference

The difference between using MaterialPageRoute in MaterialApp and CupertinoPageRoute in CupertinoApp lies in the appearance and behavior of the modal. 

When using MaterialPageRoute in MaterialApp, the modal will have a Material design appearance with platform-specific animations when opening and closing. On the other hand, using CupertinoPageRoute in CupertinoApp will give the modal a native iOS design with platform-specific animations.

To summarize:
- MaterialApp with MaterialPageRoute gives you a Material design modal on both Android and iOS.
- CupertinoApp with CupertinoPageRoute gives you a native iOS design modal on both Android and iOS.

It is important to choose the approach that is most appropriate for the design and user experience you want to achieve in your app.

# Reference
- [Flutter Navigator class documentation](https://api.flutter.dev/flutter/widgets/Navigator-class.html)