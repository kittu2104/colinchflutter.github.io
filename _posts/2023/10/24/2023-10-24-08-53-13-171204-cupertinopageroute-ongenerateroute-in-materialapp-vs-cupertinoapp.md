---
layout: post
title: "CupertinoPageRoute onGenerateRoute in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When building a Flutter application, you might encounter two similar methods: `onGenerateRoute` in `MaterialApp` and `CupertinoApp`. These methods are responsible for generating routes in your application and navigating between different screens.

## MaterialApp

`MaterialApp` is a widget used to implement Material Design in your Flutter app. It provides a set of pre-designed widgets and components that follow the Material Design guidelines.

To implement routing using `onGenerateRoute` in `MaterialApp`, you need to define a `RouteFactory` that takes in a `RouteSettings` object and returns an instance of `PageRoute`.

Here's an example of how you can use `onGenerateRoute` in `MaterialApp`:

```dart
MaterialApp(
  // ... other properties
  onGenerateRoute: (settings) {
    if (settings.name == '/screen1') {
      return MaterialPageRoute(builder: (_) => Screen1());
    } else if (settings.name == '/screen2') {
      return MaterialPageRoute(builder: (_) => Screen2());
    } else {
      return MaterialPageRoute(builder: (_) => NotFoundScreen());
    }
  },
)
```

In this example, whenever you navigate to `/screen1`, it will return an instance of `Screen1` using `MaterialPageRoute`. Similarly, `/screen2` will return `Screen2`, and any unknown route will navigate to `NotFoundScreen`.

## CupertinoApp

`CupertinoApp` is a widget used to implement the Cupertino design language, which mimics the iOS design patterns. It provides iOS-style widgets and components.

To implement routing using `onGenerateRoute` in `CupertinoApp`, you follow a similar approach as in `MaterialApp`. You define a `RouteFactory` that takes in a `RouteSettings` object and returns an instance of `PageRoute`.

Here's an example of how you can use `onGenerateRoute` in `CupertinoApp`:

```dart
CupertinoApp(
  // ... other properties
  onGenerateRoute: (settings) {
    if (settings.name == '/screen1') {
      return CupertinoPageRoute(builder: (_) => Screen1());
    } else if (settings.name == '/screen2') {
      return CupertinoPageRoute(builder: (_) => Screen2());
    } else {
      return CupertinoPageRoute(builder: (_) => NotFoundScreen());
    }
  },
)
```

The usage is similar to `MaterialApp`, but this time we are using `CupertinoPageRoute` to instantiate the routes.

## Conclusion

The main difference between `MaterialApp` and `CupertinoApp` is the design language they follow: Material Design and Cupertino (iOS) design, respectively. While the `onGenerateRoute` method works similarly in both widgets, it's essential to use the corresponding route types `MaterialPageRoute` and `CupertinoPageRoute` to ensure the consistent look and feel in your application.

Remember to choose the appropriate one based on the design patterns you want to follow for your Flutter app.

# References
- Flutter API documentation for [MaterialApp](https://api.flutter.dev/flutter/material/MaterialApp-class.html)
- Flutter API documentation for [CupertinoApp](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html)