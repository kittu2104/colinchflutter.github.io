---
layout: post
title: "MediaQuery systemGestureInsets in Flutter"
description: " "
date: 2023-10-01
tags: [MediaQuery, systemGestureInsets]
comments: true
share: true
---

In Flutter, the `MediaQuery` class is a powerful tool that allows developers to retrieve various properties and information about the device's screen. One particularly useful property that can be accessed through `MediaQuery` is the `systemGestureInsets`.

## What are systemGestureInsets?

`systemGestureInsets` represent the areas on the screen where system gestures, such as swipe gestures from the edges, can be recognized by the operating system. These insets are typically used to ensure that important UI elements, such as buttons or content, are not obstructed by system gestures.

For example, on Android devices with a navigation bar, the `systemGestureInsets` will include the area occupied by the navigation bar, ensuring that UI elements near the bottom of the screen are accessible even when the user performs swipe-up gestures.

## How to access systemGestureInsets using MediaQuery?

To retrieve the `systemGestureInsets` using `MediaQuery`, you can simply obtain an instance of `MediaQueryData` using the `MediaQuery.of(context)` method, and then access the `systemGestureInsets` property.

Here's an example on how to use `MediaQuery` to access `systemGestureInsets` in Flutter:

```dart
MediaQueryData mediaQueryData = MediaQuery.of(context);
EdgeInsets systemGestureInsets = mediaQueryData.systemGestureInsets;
```

The `systemGestureInsets` is represented by an `EdgeInsets` object that provides values for top, right, bottom, and left insets. These values denote the space occupied by the system gestures on the respective edges.

## How to use systemGestureInsets in your Flutter UI?

Once you have obtained the `systemGestureInsets`, you can utilize it to adjust your UI layout accordingly. For example, you could use it to provide additional padding or margin to your UI elements to ensure they are not obscured by system gestures.

Here's an example of how you can use `systemGestureInsets` to adjust the padding of a widget:

```dart
EdgeInsets systemGestureInsets = MediaQuery.of(context).systemGestureInsets;

Widget build(BuildContext context) {
  return Container(
    padding: EdgeInsets.only(
      bottom: systemGestureInsets.bottom,
    ),
    child: Text('Hello, World!'),
  );
}
```

In this example, we are setting the bottom padding of the `Container` widget to the value of `systemGestureInsets.bottom`, which ensures that the widget is positioned above the area occupied by system gestures.

## Conclusion

Utilizing the `MediaQuery` class in Flutter provides access to valuable information about the device's screen configuration. The `systemGestureInsets` property allows developers to account for the areas occupied by system gestures and ensure that their UI remains fully accessible and usable.

By leveraging `systemGestureInsets`, Flutter developers can create responsive and user-friendly interfaces that adapt to different device layouts and user interaction patterns.

#Flutter #MediaQuery #systemGestureInsets