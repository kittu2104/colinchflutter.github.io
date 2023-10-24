---
layout: post
title: "CupertinoPageRoute fullscreenDialog property in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When developing a Flutter application, you may come across the `fullscreenDialog` property when working with navigation. This property is used to control the appearance of a route as a full-screen dialog. 

In Flutter, there are two main ways to set up your application: using the `MaterialApp` and `CupertinoApp` widgets. These two widgets provide different design paradigms based on the target platform: Material Design for Android and web, and Cupertino Design for iOS. 

Let's explore the behavior of the `fullscreenDialog` property in both `MaterialApp` and `CupertinoApp` when navigating between routes.

## MaterialApp

When using the `MaterialApp`, the `fullscreenDialog` property is **not** supported by default. As per the Flutter documentation, this property has no effect on Android and web applications using the `MaterialApp` widget. However, it does work on iOS devices with a fallback to a regular page transition.

To enable the full-screen dialog appearance on Android and web devices, you can use the `PageRouteBuilder`. Create a custom `PageRoute` with the desired `fullscreenDialog` property and pass it as the `Page` parameter for the `MaterialPageRoute` to achieve the effect.

Example code:

```dart
Navigator.push(
  context,
  MaterialPageRoute(
    fullscreenDialog: true,
    builder: (BuildContext context) {
      // Your widget to be displayed as a full-screen dialog
    },
  ),
);
```

## CupertinoApp

On the other hand, when using the `CupertinoApp`, the `fullscreenDialog` property is supported out of the box. Setting `fullscreenDialog` to `true` will present the route as a full-screen dialog on both iOS and Android platforms.

Example code:

```dart
Navigator.push(
  context,
  CupertinoPageRoute(
    fullscreenDialog: true,
    builder: (BuildContext context) {
      // Your widget to be displayed as a full-screen dialog
    },
  ),
);
```

## Conclusion

In summary, the `fullscreenDialog` property behaves differently when using `MaterialApp` and `CupertinoApp`. 

- With `MaterialApp`, the `fullscreenDialog` property does not have an effect on Android and web platforms unless you use a custom `PageRouteBuilder`.
- With `CupertinoApp`, the `fullscreenDialog` property works as expected on both iOS and Android platforms.

Remember to consider the target platform and the appropriate design guidelines when deciding between `MaterialApp` and `CupertinoApp` in your Flutter application.