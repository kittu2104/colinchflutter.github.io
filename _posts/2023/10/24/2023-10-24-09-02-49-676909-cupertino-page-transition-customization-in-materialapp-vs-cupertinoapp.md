---
layout: post
title: "Cupertino page transition customization in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When building a Flutter application, you have two main options for the overall look and feel of your app: `MaterialApp` and `CupertinoApp`. These widgets provide different design systems and UI elements. If you want to customize the page transition animations specifically, it is important to understand the differences between the two.

## MaterialApp

`MaterialApp` is part of the Material Design system, which is the default for most Flutter applications. It provides a set of pre-built widgets and animations that follow the Material Design guidelines. By default, `MaterialApp` uses a page transition animation called `MaterialPageRoute`, which slides the new page in from the right and slides the current page out to the left.

To customize the page transition animation in `MaterialApp`, you can provide your own custom `PageRouteBuilder` to the `navigatorObservers` parameter. Here's an example:

```dart
import 'package:flutter/material.dart';

class CustomPageRoute extends PageRouteBuilder {
  final Widget page;

  CustomPageRoute({required this.page})
      : super(
          transitionDuration: Duration(milliseconds: 500),
          pageBuilder: (_, __, ___) => page,
          transitionsBuilder: (_, Animation<double> animation, __, Widget child) {
            return FadeTransition(
              opacity: animation,
              child: child,
            );
          },
        );
}

void main() {
  runApp(
    MaterialApp(
      home: Scaffold(
        body: Center(
          child: TextButton(
            child: Text('Go to Another Page'),
            onPressed: () {
              Navigator.of(context).push(CustomPageRoute(page: AnotherPage()));
            },
          ),
        ),
      ),
    ),
  );
}
```

In this example, `CustomPageRoute` extends `PageRouteBuilder` and defines a custom page transition animation. It uses the `FadeTransition` widget to fade in the new page. You can customize the animation duration and other properties to match your desired effect.

## CupertinoApp

On the other hand, `CupertinoApp` is part of the Cupertino design system, which follows the iOS design guidelines. It provides a different set of widgets and animations that give your app an iOS-like look and feel. By default, `CupertinoApp` uses a page transition animation called `CupertinoPageRoute`, which slides the new page in from the right and slides the current page out to the left, similar to `MaterialPageRoute`.

To customize the page transition animation in `CupertinoApp`, you can provide your own custom `PageRoute` to the `onGenerateRoute` parameter. Here's an example:

```dart
import 'package:flutter/cupertino.dart';

class CustomPageRoute extends PageRoute {
  final Widget page;

  CustomPageRoute({required this.page})
      : super(
          settings: RouteSettings(name: 'custom_page_route'),
        );

  @override
  Widget buildPage(BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation) {
    return FadeTransition(
      opacity: animation,
      child: page,
    );
  }

  @override
  Duration get transitionDuration => Duration(milliseconds: 500);
}

void main() {
  runApp(
    CupertinoApp(
      home: CupertinoPageScaffold(
        child: Center(
          child: CupertinoButton(
            child: Text('Go to Another Page'),
            onPressed: () {
              Navigator.of(context).push(CustomPageRoute(page: AnotherPage()));
            },
          ),
        ),
      ),
    ),
  );
}
```

In this example, `CustomPageRoute` extends `PageRoute` and defines a custom page transition animation. It uses the `FadeTransition` widget to fade in the new page. As before, you can customize the animation duration and other properties.

Note that unlike `MaterialApp`, `CupertinoApp` does not use `Navigator` directly. Instead, you can use `Navigator.of(context)` within a widget's `BuildContext` to access the navigation methods.

## Conclusion

Both `MaterialApp` and `CupertinoApp` provide options for customizing page transition animations in Flutter. While the default page transition animations are similar between the two, you can create custom animations by extending `PageRouteBuilder` for `MaterialApp` and `PageRoute` for `CupertinoApp`. 

Choosing between `MaterialApp` and `CupertinoApp` depends on the design system you want to follow (Material Design or Cupertino). Customizing page transitions in either case allows you to add your own touch and make your Flutter application feel unique. 

**References**
- Flutter Documentation: [MaterialPageRoute](https://api.flutter.dev/flutter/material/MaterialPageRoute-class.html)
- Flutter Documentation: [CupertinoPageRoute](https://api.flutter.dev/flutter/cupertino/CupertinoPageRoute-class.html)