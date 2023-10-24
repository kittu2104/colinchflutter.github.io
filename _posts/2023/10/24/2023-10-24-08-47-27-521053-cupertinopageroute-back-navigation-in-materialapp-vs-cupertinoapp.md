---
layout: post
title: "CupertinoPageRoute back navigation in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [navigation]
comments: true
share: true
---

When developing a Flutter app, you can choose between using `MaterialApp` or `CupertinoApp` as the root widget of your application. These two widgets provide different design systems: Material Design for `MaterialApp` and Cupertino for `CupertinoApp`. One key difference between them is how back navigation is handled with the `CupertinoPageRoute`.

## MaterialApp Back Navigation

In a `MaterialApp`, back navigation is managed automatically by the framework. When you push a new route onto the navigation stack using `Navigator.push`, the framework automatically adds a back button in the app bar (if available) or in the system navigation bar (if there is no app bar). This back button allows the user to go back to the previous screen.

By default, when the back button is pressed, `Navigator.pop` is called, which removes the current route from the navigation stack and navigates back to the previous route. This behavior is consistent with the Material Design guidelines and is familiar to most users.

## CupertinoApp Back Navigation

In a `CupertinoApp`, the back navigation behavior works slightly differently. When you push a new route onto the navigation stack using `Navigator.push`, the framework does not automatically add a back button. Instead, you need to handle the back navigation manually.

To handle back navigation in a `CupertinoApp`, you can use the `CupertinoPageRoute` class. This class provides a `popGesture` property, which allows you to control whether a back gesture is enabled on iOS devices. By default, the back gesture is enabled.

When the back gesture is enabled, users can swipe from the left edge of the screen to navigate back to the previous route.

```dart
Navigator.push(
  context,
  CupertinoPageRoute(
    builder: (BuildContext context) => MyPage(),
    popGesture: true, // Enable back gesture
  ),
);
```

If you want to disable the back gesture, you can set the `popGesture` property to `false`. This can be useful in some cases where you want to prevent accidental back navigation.

```dart
Navigator.push(
  context,
  CupertinoPageRoute(
    builder: (BuildContext context) => MyPage(),
    popGesture: false, // Disable back gesture
  ),
);
```

## Conclusion

In summary, when using a `MaterialApp`, the back navigation is handled automatically by the framework, while in a `CupertinoApp`, you need to manually handle back navigation using `CupertinoPageRoute`. Both approaches provide a convenient way to navigate between screens in your Flutter app, so choose the one that best fits the design system and user experience you want to achieve.

\#flutter #navigation