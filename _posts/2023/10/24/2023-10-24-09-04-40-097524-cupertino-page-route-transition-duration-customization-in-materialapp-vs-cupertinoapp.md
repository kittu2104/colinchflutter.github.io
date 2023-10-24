---
layout: post
title: "Cupertino page route transition duration customization in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When developing a Flutter application, you have the option to use either the `MaterialApp` or `CupertinoApp` widget as the root widget of your app. These widgets provide different design styles and visual components based on the target platform.

One of the key differences between `MaterialApp` and `CupertinoApp` is how they handle page route transitions and animations. In this article, we will focus specifically on customizing the duration of the page route transitions in each widget.

## Customizing Transition Duration in MaterialApp

In the `MaterialApp`, you can customize the duration of page route transitions using the `theme` property. By default, page route transitions have a duration of 300 milliseconds. To change this duration, you can define a custom `ThemeData` instance and modify the `pageTransitionsTheme` property.

Here's an example of customizing the transition duration in a `MaterialApp`:

```dart
MaterialApp(
  theme: ThemeData(
    pageTransitionsTheme: PageTransitionsTheme(
      builders: {
        TargetPlatform.android: CupertinoPageTransitionsBuilder(
          transitionDuration: Duration(milliseconds: 500),
        ),
      },
    ),
  ),
  // Rest of the app configuration
)
```

In this example, we define a custom `CupertinoPageTransitionsBuilder` with a transition duration of 500 milliseconds, targeting the Android platform. You can customize the duration for different platforms by adding more entries to the `builders` map.

## Customizing Transition Duration in CupertinoApp

In contrast, the `CupertinoApp` widget provides a simpler way to customize the duration of page route transitions. It exposes a `theme` property where you can define a custom `CupertinoThemeData` instance.

Here's an example of customizing the transition duration in a `CupertinoApp`:

```dart
CupertinoApp(
  theme: CupertinoThemeData(
    pageTransitionDuration: Duration(milliseconds: 500),
  ),
  // Rest of the app configuration
)
```

In this example, we define a custom `CupertinoThemeData` with a page transition duration of 500 milliseconds. The transition duration is applied to all page route transitions within the `CupertinoApp`.

## Conclusion

Customizing the duration of page route transitions in Flutter can be done differently depending on whether you are using `MaterialApp` or `CupertinoApp`. In `MaterialApp`, you can use the `theme` property to modify the `pageTransitionsTheme` and set custom durations for different platforms. On the other hand, `CupertinoApp` provides a simpler approach by allowing you to directly set the page transition duration through the `theme` property.

By customizing the duration of page route transitions, you can create a smoother and more engaging user experience in your Flutter applications.

# References

- Flutter API documentation - [MaterialApp](https://api.flutter.dev/flutter/material/MaterialApp-class.html)
- Flutter API documentation - [CupertinoApp](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html)