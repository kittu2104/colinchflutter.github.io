---
layout: post
title: "CupertinoNavigationBar widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

## Introduction

When developing a Flutter application, you may come across the CupertinoNavigationBar widget, which is commonly used to display a navigation bar with iOS style. It provides a sleek and familiar design for users who are accustomed to the iOS operating system.

In Flutter, there are two ways to use the CupertinoNavigationBar widget: within a MaterialApp or within a CupertinoApp. In this article, we will explore the differences between using the CupertinoNavigationBar widget with MaterialApp and CupertinoApp.

## MaterialApp

The MaterialApp widget is the entry point for many Flutter applications and provides various functionalities, such as setting the theme, defining routes, and managing the app's navigation stack. When using CupertinoNavigationBar within MaterialApp, you can simply add it as the appBar property of the MaterialApp widget.

Here's an example of how to use the CupertinoNavigationBar widget within MaterialApp:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/cupertino.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: CupertinoNavigationBar(
          middle: Text('My App'),
        ),
        body: Container(),
      ),
    );
  }
}
```

In this example, the CupertinoNavigationBar is set as the appBar property of the Scaffold widget, which is the main container for content in a Flutter screen.

## CupertinoApp

On the other hand, the CupertinoApp widget is specifically designed for iOS-style applications. It sets up the overall app structure and provides the Cupertino design language throughout the application. When using CupertinoNavigationBar within CupertinoApp, you need to provide it as the navigationBar property of the CupertinoApp widget.

Here's an example of how to use the CupertinoNavigationBar widget within CupertinoApp:

```dart
import 'package:flutter/cupertino.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoApp(
      home: CupertinoPageScaffold(
        navigationBar: CupertinoNavigationBar(
          middle: Text('My App'),
        ),
        child: Container(),
      ),
    );
  }
}
```

In this example, the CupertinoNavigationBar is set as the navigationBar property of the CupertinoPageScaffold widget, which is the primary content container in a Cupertino-style app.

## Conclusion

Both MaterialApp and CupertinoApp provide ways to use the CupertinoNavigationBar widget in Flutter applications. If you are building a cross-platform application that targets both iOS and Android, you can utilize MaterialApp. However, if you are specifically developing an iOS-style app, CupertinoApp is the recommended choice.

By understanding the use of CupertinoNavigationBar within MaterialApp and CupertinoApp, you can create a consistent and visually pleasing navigation bar in your Flutter application.

\#Flutter \#iOS