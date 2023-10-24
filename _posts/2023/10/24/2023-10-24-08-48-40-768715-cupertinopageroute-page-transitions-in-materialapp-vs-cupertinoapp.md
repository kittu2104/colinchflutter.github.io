---
layout: post
title: "CupertinoPageRoute page transitions in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When developing a Flutter application, you have the option to use either the MaterialApp or CupertinoApp widget as the root widget for your app. These two widgets provide different design patterns and aesthetics, with the MaterialApp following the Material Design guidelines and the CupertinoApp adhering to Apple's iOS design principles.

One of the key differences between these two widgets is the page transition animation they offer. Let's explore how page transitions work in MaterialApp and CupertinoApp.

## MaterialApp Page Transitions

The MaterialApp widget provides page transitions that are animated according to the Material Design guidelines. These transitions can be configured using the `PageRouteBuilder` class. For example, you can specify the animation type, duration, and curve for a specific page route.

Here's an example of how you can define a custom page transition animation in MaterialApp:

```dart
MaterialApp(
  home: MaterialPageRoute(
    builder: (context) => HomePage(),
    settings: RouteSettings(name: '/home'),
    fullscreenDialog: true,
    maintainState: true,
    maintainSize: true,
    transitionDuration: Duration(milliseconds: 500),
    transitionsBuilder: (context, animation, secondaryAnimation, child) {
      return FadeTransition(
        opacity: animation,
        child: child,
      );
    },
  ),
);
```

In the above example, we define a `FadeTransition` animation that fades the current page out and fades the new page in when navigating to the home page.

## CupertinoApp Page Transitions

On the other hand, the CupertinoApp widget provides a different set of page transition animations that align with the iOS design patterns. These transitions are automatically applied when using the `CupertinoPageRoute` class.

Here's an example of how you can use CupertinoPageRoute in a CupertinoApp:

```dart
CupertinoApp(
  home: CupertinoPageRoute(
    builder: (context) => HomePage(),
    fullscreenDialog: true,
  ),
);
```

In the above example, the `HomePage` is wrapped in a `CupertinoPageRoute` widget, which automatically applies the Cupertino-style page transition animation when navigating to the home page.

## Conclusion

The MaterialApp and CupertinoApp widgets in Flutter provide page transition animations that align with their respective design guidelines. MaterialApp offers Material Design transitions and allows more customization through `PageRouteBuilder`. On the other hand, CupertinoApp provides Cupertino-style transitions using the automatic `CupertinoPageRoute`.

Consider the user experience and the platform you are targeting when choosing between MaterialApp and CupertinoApp, as the page transition animations can enhance the overall look and feel of your app.

# References
- [Flutter documentation - MaterialApp](https://api.flutter.dev/flutter/material/MaterialApp-class.html)
- [Flutter documentation - CupertinoApp](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html)