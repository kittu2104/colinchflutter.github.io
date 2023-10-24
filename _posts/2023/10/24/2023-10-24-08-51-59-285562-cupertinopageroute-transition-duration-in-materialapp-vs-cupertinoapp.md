---
layout: post
title: "CupertinoPageRoute transition duration in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

In Flutter, there are two main widgets for creating an iOS-style user interface: MaterialApp and CupertinoApp. Each of these widgets uses different transition durations for the CupertinoPageRoute when navigating between different screens.

### MaterialApp

The MaterialApp widget is the standard way to create a material design app in Flutter. It uses the MaterialPageRoute by default when navigating between screens. The transition duration for the MaterialPageRoute in MaterialApp is controlled by the `pageTransitionsTheme` property in the MaterialApp's theme.

To change the transition duration, you can provide a custom `PageTransitionsTheme` to the `theme` property of the MaterialApp. Here's an example:

```dart
MaterialApp(
  theme: ThemeData(
    pageTransitionsTheme: PageTransitionsTheme(
      builders: {
        TargetPlatform.iOS: CupertinoPageTransitionsBuilder(
          duration: Duration(milliseconds: 500), // Set your desired duration
        ),
      },
    ),
  ),
  // Other MaterialApp properties...
)
```

In the above example, we set the transition duration to 500 milliseconds using the `duration` property of the `CupertinoPageTransitionsBuilder`.

### CupertinoApp

The CupertinoApp widget is used to create an app with an iOS-style design. When using CupertinoApp, the transition duration for the CupertinoPageRoute is controlled by the `transitionDuration` property of the CupertinoApp widget itself.

To change the transition duration, you can set the `transitionDuration` property of the CupertinoApp. Here's an example:

```dart
CupertinoApp(
  // Other CupertinoApp properties...
  transitionDuration: Duration(milliseconds: 500), // Set your desired duration
)
```

In the above example, we set the transition duration to 500 milliseconds using the `transitionDuration` property of the CupertinoApp.

### Conclusion

In summary, the transition duration for the CupertinoPageRoute in MaterialApp is controlled by the `pageTransitionsTheme` property in the MaterialApp's theme, while in CupertinoApp, it is controlled by the `transitionDuration` property of the CupertinoApp widget itself. By setting the desired duration in either of these widgets, you can customize the transition duration for navigating between screens in your Flutter app.

For more information, you can refer to the official Flutter documentation on [MaterialApp](https://api.flutter.dev/flutter/material/MaterialApp-class.html) and [CupertinoApp](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html).