---
layout: post
title: "MediaQuery orientation in Flutter"
description: " "
date: 2023-10-01
tags: [mediaqueryorientation]
comments: true
share: true
---

In Flutter, the `MediaQuery` class allows us to access various information about the device, including its orientation. The orientation can be either portrait or landscape, and knowing the current orientation can help us adjust the UI accordingly.

To get the current orientation using `MediaQuery`, we can follow these steps:

1. Import the `flutter` package:
```dart
import 'package:flutter/material.dart';
```

2. Access the orientation using `MediaQuery`:
```dart
MediaQueryData queryData = MediaQuery.of(context);
Orientation currentOrientation = queryData.orientation;
```

3. Use the `currentOrientation` value to adjust the UI based on the orientation. For example, we can conditionally modify the layout or switch between different UI components depending on the orientation:
```dart
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: Text('MediaQuery Orientation Demo'),
    ),
    body: Container(
      alignment: Alignment.center,
      child: currentOrientation == Orientation.portrait
          ? Text('This is a portrait orientation')
          : Text('This is a landscape orientation'),
    ),
  );
}
```

By using `MediaQuery` and accessing the device's orientation, we can create dynamic UIs that adapt to different screen orientations. This is particularly useful when building responsive applications that need to handle diverse device types and form factors.

#flutter #mediaqueryorientation