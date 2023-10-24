---
layout: post
title: "Cupertino page route transition customization in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When it comes to customizing page route transitions in Flutter, you have the option to choose between `MaterialApp` and `CupertinoApp`, depending on whether you want a Material Design or a Cupertino-style user interface.

## MaterialApp

`MaterialApp` is the most commonly used widget to define the root of your Flutter application when targeting material design. It provides numerous customization options, including page route transitions.

To customize the page route transitions in MaterialApp, you can make use of the `ThemeData` widget provided by Flutter. By accessing the `ThemeData` for your application, you can modify the page route transition animations. Here's an example:

```dart
MaterialApp(
  theme: ThemeData(
    pageTransitionsTheme: PageTransitionsTheme(
      builders: {
        TargetPlatform.iOS: ZoomPageTransitionsBuilder(),
        TargetPlatform.android: CupertinoPageTransitionsBuilder(),
      },
    ),
  ),
  // Other configurations for your app
);
```

In the above code snippet, we define the `pageTransitionsTheme` property of the `ThemeData`, which allows us to customize the page route transitions. We can set different transition builders based on the target platform. In this example, we set the `ZoomPageTransitionsBuilder` for iOS and the `CupertinoPageTransitionsBuilder` for Android.

## CupertinoApp

`CupertinoApp` is used to create a Cupertino-style Flutter application, which matches the design patterns of iOS. If you're aiming for an iOS-like user interface, you should use this widget instead of `MaterialApp`.

To customize the page route transitions in `CupertinoApp`, we can simply use the `PageRouteBuilder` widget, which allows us to create a custom transition for each page. Here's an example:

```dart
CupertinoApp(
  theme: CupertinoThemeData(
    pageTransitionsTheme: CupertinoPageTransitionsThemeData(
      builders: {
        PageTransitionType.primaryRoute: CupertinoPageRouteBuilder(),
        PageTransitionType.secondaryRoute: CupertinoPageRouteBuilder(),
      },
    ),
  ),
  // Other configurations for your app
);
```

In the above code snippet, we define the `pageTransitionsTheme` property of the `CupertinoThemeData`, similar to how we did it in MaterialApp. We can set different transition builders for different types of page transitions. In this example, we set the `CupertinoPageRouteBuilder` for both primary and secondary route transitions.

## Conclusion

Both `MaterialApp` and `CupertinoApp` provide options to customize page route transitions in Flutter. MaterialApp utilizes the `ThemeData` widget to define transition builders, while CupertinoApp uses the `PageRouteBuilder` to customize transitions for each page.

By choosing the appropriate widget based on your desired UI style (Material Design or Cupertino), you can easily customize the page route transitions in your Flutter application.

# References

- [Flutter Documentation - MaterialApp](https://api.flutter.dev/flutter/material/MaterialApp-class.html)
- [Flutter Documentation - CupertinoApp](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html)