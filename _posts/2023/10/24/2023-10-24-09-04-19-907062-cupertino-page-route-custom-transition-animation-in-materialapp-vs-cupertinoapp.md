---
layout: post
title: "Cupertino page route custom transition animation in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [materialdesign, cupertino]
comments: true
share: true
---

When building a Flutter application, you have the option to use either the `MaterialApp` or `CupertinoApp` widget as the root of your app. Both widgets provide different UI styles based on the design guidelines of either Android (Material design) or iOS (Cupertino design).

One key difference between the two widgets is the default transition animation used when navigating between screens. In a `MaterialApp`, the default animation is a fade-in/fade-out effect, whereas in a `CupertinoApp`, it is a slide animation.

However, if you are using a `MaterialApp` and want to achieve the slide animation transition effect similar to `CupertinoApp`, you can customize the page route transition animation. This can be done using the `PageRouteBuilder` class.

To add a custom transition animation in a `MaterialApp`, you can define your own `PageRouteBuilder` and set it as the `pageRouteBuilder` property of your `MaterialApp`. Here's an example:

```dart
import 'package:flutter/material.dart';

class CustomPageRoute<T> extends MaterialPageRoute<T> {
  CustomPageRoute({required WidgetBuilder builder, required RouteSettings settings})
      : super(builder: builder, settings: settings);

  @override
  Widget buildTransitions(BuildContext context, Animation<double> animation,
      Animation<double> secondaryAnimation, Widget child) {
    return SlideTransition(
      position: Tween<Offset>(
        begin: const Offset(1.0, 0.0),
        end: Offset.zero,
      ).animate(animation),
      child: child,
    );
  }
}

void main() {
  runApp(MaterialApp(
    initialRoute: '/',
    routes: {
      '/': (context) => FirstScreen(),
      '/second': (context) => SecondScreen(),
    },
    pageRouteBuilder: <T>(RouteSettings settings, WidgetBuilder builder) {
      return CustomPageRoute(builder: builder, settings: settings);
    },
  ));
}
```

In the code above, we're creating a custom `PageRoute` called `CustomPageRoute` that uses `SlideTransition` to create a slide-in animation. The `SlideTransition` animates the `child` widget from an initial offset of `Offset(1.0, 0.0)` to `Offset.zero` based on the provided `animation`.

We then set `CustomPageRoute` as the `pageRouteBuilder` of the `MaterialApp` and define our routes using the `routes` property.

If you want to achieve the default slide animation transition in a `CupertinoApp`, you don't need to make any additional changes as it is the default behavior.

That's it! Now you can customize the page route transition animation in a `MaterialApp` to match the slide animation effect of `CupertinoApp`. Happy coding!

**References:**
- Flutter API documentation: [PageRouteBuilder](https://api.flutter.dev/flutter/widgets/PageRouteBuilder-class.html)
- Flutter API documentation: [MaterialApp](https://api.flutter.dev/flutter/material/MaterialApp-class.html)
- Flutter API documentation: [CupertinoApp](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html)

---

#flutter #materialdesign #cupertino