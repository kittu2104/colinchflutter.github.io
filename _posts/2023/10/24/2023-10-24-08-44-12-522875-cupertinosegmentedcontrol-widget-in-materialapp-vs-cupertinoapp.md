---
layout: post
title: "CupertinoSegmentedControl widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [segmentedcontrol]
comments: true
share: true
---

With the release of Flutter 2.0, developers have access to a variety of widgets that provide a native look and feel across different platforms. Two popular widgets that are frequently used to create segmented controls are `CupertinoSegmentedControl` and `CupertinoApp`. While both widgets offer similar functionality, they have some distinct differences when used with `MaterialApp` and `CupertinoApp`.

### CupertinoSegmentedControl

The `CupertinoSegmentedControl` widget is specifically designed for iOS-style segmented controls. It allows you to create a group of segmented buttons with customizable labels and corresponding values. This widget follows Apple's Human Interface Guidelines for iOS and provides a consistent user experience.

To use `CupertinoSegmentedControl` in your application, you need to wrap it within a `CupertinoApp` widget. The `CupertinoSegmentedControl` works seamlessly within the `CupertinoApp` environment and provides the expected iOS-style segmented control.

```dart
CupertinoApp(
  home: Scaffold(
    appBar: CupertinoNavigationBar(
      middle: Text('Segmented Control Demo'),
    ),
    body: Column(
      children: [
        CupertinoSegmentedControl(
          children: {
            0: Text('Option 1'),
            1: Text('Option 2'),
            2: Text('Option 3'),
          },
          onValueChanged: (value) {
            // Handle value change
          },
        ),
        // Other widgets
      ],
    ),
  ),
)
```

### CupertinoApp

On the other hand, the `CupertinoApp` widget is the top-level widget for iOS-styled apps in Flutter. It provides the overall design and behavior of an iOS app, including the navigation bar, scrolling behavior, and default stylings.

When using the `CupertinoApp`, you can still use the `CupertinoSegmentedControl` widget. However, it is important to note that it will not provide the exact look and feel as when used with a `CupertinoApp`.

```dart
MaterialApp(
  home: Scaffold(
    appBar: CupertinoNavigationBar(
      middle: Text('Segmented Control Demo'),
    ),
    body: Column(
      children: [
        CupertinoSegmentedControl(
          children: {
            0: Text('Option 1'),
            1: Text('Option 2'),
            2: Text('Option 3'),
          },
          onValueChanged: (value) {
            // Handle value change
          },
        ),
        // Other widgets
      ],
    ),
  ),
)
```

As you can see, when using `CupertinoSegmentedControl` with `MaterialApp`, it still provides basic functionality, but the styling will follow the Material Design guidelines rather than the iOS guidelines.

In conclusion, if you are developing an app specifically for iOS and want to create iOS-styled segmented controls, using the `CupertinoSegmentedControl` within a `CupertinoApp` is the recommended approach. However, if you are building a cross-platform app and want to maintain a consistent look and feel across both iOS and Android, you may want to consider using the `MaterialApp` with `CupertinoSegmentedControl` for a unified design.

**References:**
- Flutter CupertinoSegmentedControl documentation: [https://api.flutter.dev/flutter/cupertino/CupertinoSegmentedControl-class.html](https://api.flutter.dev/flutter/cupertino/CupertinoSegmentedControl-class.html)
- Flutter CupertinoApp documentation: [https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html)

**#flutter #segmentedcontrol**