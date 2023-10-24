---
layout: post
title: "Cupertino page route hero animation customization in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [HeroAnimations]
comments: true
share: true
---

When working with Flutter, you have the option to choose between two main widget classes to build your app's user interface: `MaterialApp` and `CupertinoApp`. These two classes provide their own set of predefined widgets and offer slightly different customization options.

One key difference between the two is how the hero animation is handled when navigating between routes. In this blog post, we will focus specifically on customizing the hero animation in both `MaterialApp` and `CupertinoApp` and explore the differences between them.

## Table of Contents
- [Introduction](#introduction)
- [Customizing Hero Animations in MaterialApp](#customizing-hero-animations-in-materialapp)
- [Customizing Hero Animations in CupertinoApp](#customizing-hero-animations-in-cupertinoapp)
- [Conclusion](#conclusion)

## Introduction

Hero animations are a popular feature that provides seamless transitions between routes by animating a shared element from one route to another. With Flutter, you can customize the hero animation to match the design and style of your app.

## Customizing Hero Animations in MaterialApp

In `MaterialApp`, you can customize the hero animations using the `PageRouteBuilder` class. By creating a custom route and overriding the `buildTransitions` method, you have full control over how the animation behaves.

Here's an example of customizing the hero animation in `MaterialApp`:

```dart
MaterialApp(
  // Other MaterialApp properties...
  onGenerateRoute: (settings) {
    if (settings.name == '/myRoute') {
      return PageRouteBuilder(
        pageBuilder: (context, animation, secondaryAnimation) {
          // Return the widget for your custom route
        },
        transitionsBuilder: (context, animation, secondaryAnimation, child) {
          return FadeTransition(
            opacity: animation,
            child: child,
          );
        },
      );
    }
    return null;
  },
)
```

In the above code, the `PageRouteBuilder` is used to create a custom route. The `transitionsBuilder` property dictates the hero animation behavior, and in this example, a fade transition is used.

## Customizing Hero Animations in CupertinoApp

With `CupertinoApp`, customizing the hero animation is a little different. Instead of using `PageRouteBuilder`, you can directly customize the navigation transition using the `CupertinoPageRoute` class.

Here's an example of customizing the hero animation in `CupertinoApp`:

```dart
CupertinoApp(
  // Other CupertinoApp properties...
  onGenerateRoute: (settings) {
    if (settings.name == '/myRoute') {
      return CupertinoPageRoute(
        builder: (context) {
          // Return the widget for your custom route
        },
        fullscreenDialog: true,
        settings: settings,
      );
    }
    return null;
  },
)
```

In the code snippet above, the `CupertinoPageRoute` is used to create a custom route. You can provide the widget for your custom route using the `builder` property. Additionally, you can control whether the custom route should be displayed as a fullscreen dialog using the `fullscreenDialog` property.

## Conclusion

Both `MaterialApp` and `CupertinoApp` provide ways to customize the hero animations when navigating between routes. By using `PageRouteBuilder` in `MaterialApp` or `CupertinoPageRoute` in `CupertinoApp`, you can have full control over the animation behavior.

The choice between `MaterialApp` and `CupertinoApp` depends on the design and user experience you want to achieve in your app. If you want an iOS-like look and feel, consider using `CupertinoApp`; otherwise, `MaterialApp` is a great option.

Remember to leverage the flexibility and customization options available in Flutter to create stunning hero animations that enhance the overall user experience of your app.

**#Flutter** **#HeroAnimations**