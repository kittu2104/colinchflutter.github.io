---
layout: post
title: "Tappable widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When building a mobile app with Flutter, you have the option to choose between `MaterialApp` and `CupertinoApp` as the root widget for your application. Both provide a wide range of widgets and styles, but there are some differences when it comes to creating tappable widgets.

## MaterialApp

`MaterialApp` is the default choice for building Android-like applications in Flutter. It follows the Material Design guidelines, providing a set of widgets with ready-made styles and animations.

To create a tappable widget in `MaterialApp`, you can use the `InkWell` widget. The `InkWell` widget provides an ink splash effect when tapped, giving visual feedback to the user. Here's an example of how you can use `InkWell` within a `MaterialApp`:

```dart
MaterialApp(
  home: Scaffold(
    appBar: AppBar(
      title: Text('My App'),
    ),
    body: Center(
      child: InkWell(
        onTap: () {
          // Handle tap event
        },
        child: Container(
          width: 200,
          height: 50,
          decoration: BoxDecoration(
            color: Colors.blue,
            borderRadius: BorderRadius.circular(10),
          ),
          child: Center(
            child: Text(
              'Tap me',
              style: TextStyle(
                color: Colors.white,
                fontSize: 20,
              ),
            ),
          ),
        ),
      ),
    ),
  ),
)
```

In this example, the `InkWell` widget wraps a `Container` to create a tappable area with a blue background and rounded corners. The `onTap` callback is triggered when the container is tapped, allowing you to handle the tap event and perform any desired actions.

## CupertinoApp

On the other hand, if you want to create an iOS-like application in Flutter, you can use the `CupertinoApp` widget. It follows the Apple Human Interface Guidelines, providing a set of widgets and styles specific to iOS.

To create a tappable widget in `CupertinoApp`, you can use the `GestureDetector` widget. The `GestureDetector` widget allows you to detect various touch gestures, including taps. Here's an example of how you can use `GestureDetector` within a `CupertinoApp`:

```dart
CupertinoApp(
  home: CupertinoPageScaffold(
    navigationBar: CupertinoNavigationBar(
      middle: Text('My App'),
    ),
    child: Center(
      child: GestureDetector(
        onTap: () {
          // Handle tap event
        },
        child: Container(
          width: 200,
          height: 50,
          decoration: BoxDecoration(
            color: CupertinoColors.activeBlue,
            borderRadius: BorderRadius.circular(10),
          ),
          child: Center(
            child: Text(
              'Tap me',
              style: TextStyle(
                color: CupertinoColors.white,
                fontSize: 20,
              ),
            ),
          ),
        ),
      ),
    ),
  ),
)
```

In this example, the `GestureDetector` widget is used to wrap a `Container` and detect the tap gesture. The container has a blue background, rounded corners, and displays the text "Tap me". Similarly to `InkWell`, you can handle the tap event by providing a callback to the `onTap` property.

Overall, both `MaterialApp` and `CupertinoApp` provide options for creating tappable widgets in Flutter. When choosing between them, consider the design guidelines of the platform you are targeting and use the appropriate widgets accordingly.

<div align="center"><b>References:</b></div>

- MaterialApp documentation: [https://api.flutter.dev/flutter/material/MaterialApp-class.html](https://api.flutter.dev/flutter/material/MaterialApp-class.html)
- CupertinoApp documentation: [https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html)
- InkWell documentation: [https://api.flutter.dev/flutter/material/InkWell-class.html](https://api.flutter.dev/flutter/material/InkWell-class.html)
- GestureDetector documentation: [https://api.flutter.dev/flutter/widgets/GestureDetector-class.html](https://api.flutter.dev/flutter/widgets/GestureDetector-class.html)