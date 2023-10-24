---
layout: post
title: "CupertinoPageRoute named routes in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When working with Flutter, you have the ability to define named routes for easy navigation within your app. Named routes allow you to navigate to specific screens using a unique identifier, rather than manually managing the navigation stack.

In Flutter, you can define named routes in both `MaterialApp` and `CupertinoApp`, which are widgets used to configure the overall theme and navigation structure of your app.

### MaterialApp

`MaterialApp`, as the name suggests, is used for building apps with a Material Design look and feel. It provides a set of widgets and components that follow the Material Design guidelines. When using `MaterialApp`, you can define named routes using the `routes` parameter in the constructor.

```dart
void main() {
  runApp(MaterialApp(
    routes: {
      '/home': (context) => HomePage(),
      '/profile': (context) => ProfilePage(),
    },
    home: HomePage(),
  ));
}
```

In the example above, we define two named routes `/home` and `/profile`. We map each route to its corresponding widget class. The `home` parameter is used to specify the default route when the app is first launched.

To navigate to a named route, you can use the `Navigator` class provided by Flutter. For example, you can use `Navigator.pushNamed()` to navigate to the `/profile` route:

```dart
Navigator.pushNamed(context, '/profile');
```

### CupertinoApp

`CupertinoApp`, on the other hand, is used for building apps with an iOS-like design. It follows the Cupertino widget style, which provides iOS-specific widgets and components. Like `MaterialApp`, `CupertinoApp` also allows you to define named routes using the `routes` parameter.

```dart
void main() {
  runApp(CupertinoApp(
    routes: {
      '/home': (context) => HomePage(),
      '/profile': (context) => ProfilePage(),
    },
    home: HomePage(),
  ));
}
```

The `routes` parameter is defined in a similar way as `MaterialApp`, allowing you to map named routes to their respective widget classes.

To navigate to a named route in a `CupertinoApp`, you can also use the `Navigator` class. The only difference is that you need to use `CupertinoPageRoute` instead of the default `MaterialPageRoute`. For example:

```dart
Navigator.push(context, CupertinoPageRoute(builder: (context) => ProfilePage()));
```

### Key Differences

The main difference between using named routes in `MaterialApp` and `CupertinoApp` is the visual style of the app. `MaterialApp` provides a Material Design look and feel, while `CupertinoApp` provides an iOS-like design. The choice between the two mainly depends on the platform you are targeting and the design language you want to follow.

Remember, whether you choose `MaterialApp` or `CupertinoApp`, the concept of named routes and how to use them remains the same. It's just the visual representation that differs.

To summarize, both `MaterialApp` and `CupertinoApp` support named routes, allowing you to define a navigation structure for your app. Understanding the visual differences between the two will help you choose the appropriate widget for your app's design and UX.

### References

- [Flutter Documentation - MaterialApp](https://api.flutter.dev/flutter/material/MaterialApp-class.html)
- [Flutter Documentation - CupertinoApp](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html)