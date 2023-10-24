---
layout: post
title: "CupertinoPageRoute modal presentation in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When developing a mobile application using Flutter, you have the flexibility to choose between two different app widgets: MaterialApp and CupertinoApp. Both of these widgets provide a set of components and design patterns specific to either Material Design (Android) or Cupertino (iOS) style.

One key difference between MaterialApp and CupertinoApp is how modals are presented. In this blog post, we will explore the different modal presentation styles when using CupertinoPageRoute with MaterialApp and CupertinoApp.

## Modal Presentation in MaterialApp

In MaterialApp, modals are presented using the MaterialPageRoute class, which is part of the material library. This class provides a standard Material Design modal presentation on both Android and iOS.

To present a modal using MaterialPageRoute in MaterialApp, you can use the Navigator widget's push method. Here's an example code snippet:

```dart
Navigator.push(
  context,
  MaterialPageRoute(
    builder: (context) => MyModalScreen(),
    fullscreenDialog: true,
  ),
);
```

In the above code, MyModalScreen is the widget representing your modal screen. The `fullscreenDialog` parameter determines whether the modal should take up the entire screen or partially cover the previous screen.

## Modal Presentation in CupertinoApp

In CupertinoApp, modals are presented using the CupertinoPageRoute class, which is part of the cupertino library. This class provides a modal presentation style consistent with the Cupertino (iOS) design guidelines.

To present a modal using CupertinoPageRoute in CupertinoApp, you can also use the Navigator widget's push method. Here's an example code snippet:

```dart
Navigator.push(
  context,
  CupertinoPageRoute(
    builder: (context) => MyModalScreen(),
    fullscreenDialog: true,
  ),
);
```

The code to present a modal is quite similar to using MaterialPageRoute in MaterialApp. However, behind the scenes, CupertinoPageRoute will provide a modal presentation style that adheres to the Cupertino design guidelines, giving your iOS app a native feel.

## Conclusion

Choosing between MaterialApp and CupertinoApp is largely dependent on the specific design styles and patterns you want to implement in your Flutter app. Both MaterialApp and CupertinoApp offer a straightforward way to present modals using MaterialPageRoute and CupertinoPageRoute classes, respectively.

Regardless of your choice, Flutter provides a convenient and flexible framework for creating beautiful and native-like modal presentations on both Android and iOS.

# References

- Flutter MaterialApp documentation: [link](https://api.flutter.dev/flutter/material/MaterialApp-class.html)
- Flutter CupertinoApp documentation: [link](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html)
- Flutter Navigator documentation: [link](https://api.flutter.dev/flutter/widgets/Navigator-class.html)
- Flutter MaterialPageRoute documentation: [link](https://api.flutter.dev/flutter/material/MaterialPageRoute-class.html)
- Flutter CupertinoPageRoute documentation: [link](https://api.flutter.dev/flutter/cupertino/CupertinoPageRoute-class.html)