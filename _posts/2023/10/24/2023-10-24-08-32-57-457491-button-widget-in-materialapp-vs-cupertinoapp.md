---
layout: post
title: "Button widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

In Flutter, there are two main widget libraries for creating mobile apps: MaterialApp and CupertinoApp. These libraries provide a set of widgets with different styling options based on the material design guidelines for Android (MaterialApp) and the iOS design guidelines (CupertinoApp). One of the most commonly used widgets in both libraries is the button widget.

## MaterialApp Button Widget
The button widget in the MaterialApp library follows the material design guidelines and provides a wide range of customization options. It is represented by the `ElevatedButton` or `TextButton` widgets. 

### ElevatedButton
The `ElevatedButton` widget renders a raised button with a shadow effect. It is typically used for primary actions in the app. Here's an example code snippet:

```dart
ElevatedButton(
  onPressed: () {
    // Action to be performed when the button is pressed
  },
  child: Text('Submit'),
)
```

### TextButton
The `TextButton` widget is a simple button with no background color or shadow. It is often used for secondary or less prominent actions. 

```dart
TextButton(
  onPressed: () {
    // Action to be performed when the button is pressed
  },
  child: Text('Cancel'),
)
```

## CupertinoApp Button Widget
The button widget in the CupertinoApp library follows the iOS design guidelines and provides a consistent iOS-style look and feel. It is represented by the `CupertinoButton` widget.

```dart
CupertinoButton(
  onPressed: () {
    // Action to be performed when the button is pressed
  },
  child: Text('Save'),
)
```

The `CupertinoButton` widget is typically used for actions within an iOS app and offers a range of customization options such as different button styles and colors.

## Conclusion
Choosing between the button widgets in MaterialApp and CupertinoApp depends on the design and platform consistency you want to achieve in your app. If you are building a cross-platform app and want to follow material design guidelines, the MaterialApp button widgets are a good choice. On the other hand, if you are targeting iOS devices and want to adhere to iOS design guidelines, the CupertinoApp button widget is the way to go.

It's worth noting that both MaterialApp and CupertinoApp libraries provide a rich set of widgets beyond buttons, allowing you to build comprehensive and platform-specific user interfaces.