---
layout: post
title: "CupertinoPageRoute custom transitions in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When building a Flutter application, you have the option to use either `MaterialApp` or `CupertinoApp` as the root widget for your app. These two widgets provide different themes and visual designs: `MaterialApp` follows the Material Design guidelines, while `CupertinoApp` follows the iOS design guidelines.

One aspect where these two widgets differ is in the default transition animations used when navigating between screens. `MaterialApp` uses a standard slide animation, while `CupertinoApp` uses a vertical slide animation with a fade effect. However, in both cases, you can customize the transitions by using the `PageRouteBuilder` and `CupertinoPageRoute` classes.

To create custom transitions in `MaterialApp`, you can use the `PageRouteBuilder` class. Here's an example:

```dart
MaterialApp(
  home: MyHomePage(),
  onGenerateRoute: (settings) {
    return PageRouteBuilder(
      pageBuilder: (context, animation, secondaryAnimation) {
        return MyPage();
      },
      transitionsBuilder: (context, animation, secondaryAnimation, child) {
        return SlideTransition(
          position: Tween<Offset>(
            begin: Offset(1, 0),
            end: Offset.zero,
          ).animate(animation),
          child: child,
        );
      },
    );
  },
)
```

In the above example, we define `PageRouteBuilder` as the `onGenerateRoute` callback of `MaterialApp`. Inside `PageRouteBuilder`, we specify the `pageBuilder` callback which returns the widget representing the destination page, and the `transitionsBuilder` callback which returns the widget representing the transition animation.

To create custom transitions in `CupertinoApp`, you can use the `CupertinoPageRoute` class. Here's an example:

```dart
CupertinoApp(
  home: MyHomePage(),
  onGenerateRoute: (settings) {
    return CupertinoPageRoute(
      builder: (context) {
        return MyPage();
      },
      fullscreenDialog: false,
      transitionsBuilder: (context, animation, secondaryAnimation, child) {
        return FadeTransition(
          opacity: animation,
          child: SlideTransition(
            position: Tween<Offset>(
              begin: Offset(0, 1),
              end: Offset.zero,
            ).animate(animation),
            child: child,
          ),
        );
      },
    );
  },
)
```

In this example, we define `CupertinoPageRoute` as the `onGenerateRoute` callback of `CupertinoApp`. We provide the `builder` callback to define the widget representing the destination page, and the `transitionsBuilder` callback to define the transition animation. 

You can customize the animation by using different transition widgets like `SlideTransition`, `FadeTransition`, etc. You can also specify additional properties like `fullscreenDialog` for the dialog-style presentation effect, similar to iOS.

Both `MaterialApp` and `CupertinoApp` provide a flexible way to create custom transitions between screens in your Flutter application. Use them according to your design needs and target platform guidelines.

For more information, you can refer to the official Flutter documentation:
- [MaterialApp class](https://api.flutter.dev/flutter/material/MaterialApp-class.html)
- [CupertinoApp class](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html)
- [PageRouteBuilder class](https://api.flutter.dev/flutter/widgets/PageRouteBuilder-class.html)
- [CupertinoPageRoute class](https://api.flutter.dev/flutter/cupertino/CupertinoPageRoute-class.html)