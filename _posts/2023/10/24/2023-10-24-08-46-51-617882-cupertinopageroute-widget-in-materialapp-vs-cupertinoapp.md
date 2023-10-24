---
layout: post
title: "CupertinoPageRoute widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When developing mobile applications with Flutter, you may come across two different widgets that are commonly used for navigation: `CupertinoPageRoute` and `CupertinoApp`. While both widgets are part of the Cupertino library and provide a similar navigation experience with iOS-style transitions, they are used in slightly different scenarios.

## MaterialApp

`MaterialApp` is the main widget used for building applications in Flutter. It provides a Material Design-themed user interface and incorporates various Material widgets, including navigation widgets like `MaterialPageRoute`.

The `MaterialPageRoute` is the default navigation widget used by `MaterialApp`, and it is optimized for Material Design guidelines. It provides transitions like slide and fade when navigating between screens, and it is suitable for both Android and iOS applications.

Here's an example of how to use `MaterialApp` with `MaterialPageRoute`:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    home: HomePage(),
    routes: {
      '/second': (context) => SecondPage(),
    },
  ));
}

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Home'),
      ),
      body: Center(
        child: RaisedButton(
          onPressed: () {
            Navigator.pushNamed(context, '/second');
          },
          child: Text('Go to Second Page'),
        ),
      ),
    );
  }
}

class SecondPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Second Page'),
      ),
      body: Center(
        child: RaisedButton(
          onPressed: () {
            Navigator.pop(context);
          },
          child: Text('Go back'),
        ),
      ),
    );
  }
}
```

## CupertinoApp

On the other hand, if you want your application to have an iOS-specific look and feel, you can use the `CupertinoApp` widget. It provides an iOS-style user interface with Cupertino widgets, including the `CupertinoPageRoute` for navigation.

The `CupertinoPageRoute` widget offers iOS-style transitions like fade, zoom, and cupertino dialogs. It is specifically designed to match the native iOS experience and is more suitable for applications that primarily target iOS devices.

Here's an example of how to use `CupertinoApp` with `CupertinoPageRoute`:

```dart
import 'package:flutter/cupertino.dart';

void main() {
  runApp(CupertinoApp(
    home: HomePage(),
    routes: {
      '/second': (context) => SecondPage(),
    },
  ));
}

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(
        middle: Text('Home'),
      ),
      child: Center(
        child: CupertinoButton(
          onPressed: () {
            Navigator.pushNamed(context, '/second');
          },
          child: Text('Go to Second Page'),
        ),
      ),
    );
  }
}

class SecondPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(
        middle: Text('Second Page'),
      ),
      child: Center(
        child: CupertinoButton(
          onPressed: () {
            Navigator.pop(context);
          },
          child: Text('Go back'),
        ),
      ),
    );
  }
}
```

In conclusion, if you are building a cross-platform application or aiming for a Material Design-themed UI, you can use `MaterialApp` with `MaterialPageRoute`. However, if you want to create an application with an iOS-specific design, `CupertinoApp` with `CupertinoPageRoute` is the way to go. Remember to choose the appropriate widget based on your target platform to provide a consistent user experience.

#flutter #ios