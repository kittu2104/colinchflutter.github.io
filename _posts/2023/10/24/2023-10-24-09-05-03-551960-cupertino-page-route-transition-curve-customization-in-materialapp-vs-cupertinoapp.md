---
layout: post
title: "Cupertino page route transition curve customization in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

In Flutter, both the MaterialApp and CupertinoApp widgets offer a way to customize the page route transition curve. These curves define how the transition animation between different screens is performed. While both MaterialApp and CupertinoApp provide this customization option, there are subtle differences in how it is achieved.

## MaterialApp

The MaterialApp widget is the most commonly used widget for creating Material Design apps in Flutter. To customize the page route transition curve in MaterialApp, you need to wrap your MaterialApp widget with a PageTransitionsTheme widget and set the desired transition curve.

Here's an example code snippet that demonstrates how to customize the transition curve using MaterialApp:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: ThemeData(
        pageTransitionsTheme: PageTransitionsTheme(
          builders: {
            TargetPlatform.android: CupertinoPageTransitionsBuilder(),
          },
        ),
      ),
      home: HomeScreen(),
    );
  }
}

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Home'),
      ),
      body: Center(
        child: Text('Welcome to the Home Screen'),
      ),
    );
  }
}
```

In the above code, we set the pageTransitionsTheme property of the ThemeData to a PageTransitionsTheme with a custom transition builder. Here, we use CupertinoPageTransitionsBuilder to achieve a Cupertino-style transition curve even in a MaterialApp-based app.

## CupertinoApp

The CupertinoApp widget is used for creating iOS-styled apps in Flutter. Similar to MaterialApp, CupertinoApp also allows for customizing the page route transition curve.

Here's an example code snippet that demonstrates how to customize the transition curve using CupertinoApp:

```dart
import 'package:flutter/cupertino.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoApp(
      theme: CupertinoThemeData(
        pageTransitionsTheme: CupertinoPageTransitionsThemeData(
          builder: CupertinoPageTransitionsBuilder(),
        ),
      ),
      home: HomeScreen(),
    );
  }
}

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(
        middle: Text('Home'),
      ),
      child: Center(
        child: Text('Welcome to the Home Screen'),
      ),
    );
  }
}
```

In the above code, we set the pageTransitionsTheme property of the CupertinoThemeData to a CupertinoPageTransitionsThemeData with a custom transition builder. Here, we also use CupertinoPageTransitionsBuilder to achieve a Cupertino-style transition curve.

## Conclusion

Both MaterialApp and CupertinoApp provide options to customize the page route transition curve. By using the PageTransitionsTheme in MaterialApp or the pageTransitionsTheme in CupertinoThemeData for CupertinoApp, you can ensure that the transition animation is tailored to your app's design and style.

Remember that the choice between MaterialApp and CupertinoApp depends on the desired design language. MaterialApp gives you access to the Material Design styles, while CupertinoApp brings the iOS-style experience. Choose the appropriate one based on the platform you are targeting.

# References
- [Flutter Material Design documentation](https://flutter.dev/docs/development/ui/widgets/material)
- [Flutter Cupertino (iOS-style) Widgets documentation](https://flutter.dev/docs/development/ui/widgets/cupertino)