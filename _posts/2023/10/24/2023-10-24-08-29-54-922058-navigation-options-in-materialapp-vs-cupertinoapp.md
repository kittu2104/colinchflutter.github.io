---
layout: post
title: "Navigation options in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [navigation]
comments: true
share: true
---

When building a mobile app with Flutter, you have the option to use either `MaterialApp` or `CupertinoApp` as the root widget for your application. Both of these widgets provide different navigation options that you can configure based on the design language you want to follow.

## MaterialApp

The `MaterialApp` widget is primarily used for building apps that follow the Material Design guidelines. It provides a set of navigation options that are suited for this design language. Here are some of the navigation options available in `MaterialApp`:

### MaterialApp class

- `initialRoute`: The initial route that is displayed when the app starts.
- `routes`: A map of named routes in the app, which can be used to navigate to different screens using `Navigator.pushNamed()`.
- `onGenerateRoute`: A callback that is invoked when navigating to a named route that is not defined in the `routes` map.
- `onUnknownRoute`: A callback that is invoked when navigating to an undefined route.

### Navigator class

- `push`: Pushes a new route onto the navigation stack.
- `pushReplacement`: Replaces the current route in the navigation stack with a new one.
- `pop`: Pops the top route from the navigation stack.

## CupertinoApp

On the other hand, if you prefer to follow the Cupertino design language (used in iOS apps), you can use the `CupertinoApp` widget as the root of your app. `CupertinoApp` provides navigation options that are specifically designed for this style. Here are some of the navigation options available in `CupertinoApp`:

### CupertinoApp class

- `initialRoute`: The initial route that is displayed when the app starts.
- `routes`: A map of named routes in the app, which can be used to navigate to different screens using `Navigator.pushNamed()`.
- `onGenerateRoute`: A callback that is invoked when navigating to a named route that is not defined in the `routes` map.
- `onUnknownRoute`: A callback that is invoked when navigating to an undefined route.

### Navigator class

- `push`: Pushes a new route onto the navigation stack.
- `pushReplacement`: Replaces the current route in the navigation stack with a new one.
- `pop`: Pops the top route from the navigation stack.

## Conclusion

Both `MaterialApp` and `CupertinoApp` provide similar navigation options in terms of routes and navigation stack manipulation. The difference lies in the design language they follow. If you are building an app that adheres to the Material Design guidelines, `MaterialApp` is the way to go. On the other hand, if you want to create an iOS-like experience using Cupertino design, choose `CupertinoApp`. #flutter #navigation