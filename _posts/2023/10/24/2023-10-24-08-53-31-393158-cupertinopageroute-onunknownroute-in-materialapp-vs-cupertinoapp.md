---
layout: post
title: "CupertinoPageRoute onUnknownRoute in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When developing mobile applications using Flutter, you have the choice between two different widget libraries for the user interface: MaterialApp and CupertinoApp. These widget libraries offer different design styles based on the platform – MaterialApp follows Material Design guidelines for Android, while CupertinoApp follows the iOS design principles.

One noteworthy difference between the two is the way they handle unknown routes. In MaterialApp, you can define an `onUnknownRoute` callback to handle navigation to routes that are not registered. For example:

```dart
MaterialApp(
  onUnknownRoute: (settings) =>
    MaterialPageRoute(builder: (_) => UnknownRoutePage()),
  // ...
)
```

In the code snippet above, when a route is not recognized by the MaterialApp, the `onUnknownRoute` callback will be called, and you can handle this situation by returning a new MaterialPageRoute with the appropriate route.

On the other hand, CupertinoApp does not provide a direct `onUnknownRoute` callback. Instead, it relies on the `navigatorKey` property of CupertinoApp, which is used to navigate between routes. You can use this key to handle unknown routes by setting a custom `onGenerateRoute` callback:

```dart
CupertinoApp(
  navigatorKey: GlobalKey<NavigatorState>(),
  // ...
  onGenerateRoute: (settings) {
    final routeName = settings.name;
    if (routeName == '/unknown') {
      return CupertinoPageRoute(builder: (_) => UnknownRoutePage());
    }
    // Handling other routes...
  },
  // ...
)
```

Here, when the route is not recognized, you can manually create a new CupertinoPageRoute and return it from the `onGenerateRoute` callback.

It's essential to note that this difference in handling unknown routes is due to the design philosophy of each platform. When using MaterialApp, you have more control over navigation and routing, whereas with CupertinoApp, the navigation is primarily managed by the CupertinoPageScaffold and CupertinoTabScaffold widgets.

In summary, if you need to handle unknown routes in MaterialApp, you can use the `onUnknownRoute` callback, while in CupertinoApp, you need to set a custom `onGenerateRoute` callback using the `navigatorKey` property. Understanding these differences will enable you to choose the appropriate widget library based on the design requirements of your Flutter application.

**References:**
- MaterialApp class - Flutter API documentation: [https://api.flutter.dev/flutter/material/MaterialApp-class.html](https://api.flutter.dev/flutter/material/MaterialApp-class.html)
- CupertinoApp class - Flutter API documentation: [https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html)