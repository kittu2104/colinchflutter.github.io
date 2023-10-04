---
layout: post
title: "How to disable animations using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [Animations]
comments: true
share: true
---

Animations bring life to apps, but there might be instances where you want to disable them for various reasons. In Flutter, you can disable animations using the `MediaQuery` class. In this blog post, we will guide you through the process of disabling animations using `MediaQuery` in your Flutter app.

## What is MediaQuery?

`MediaQuery` is a class in Flutter that provides information about the current screen, such as its size, pixel density, orientation, and more. It allows you to access and modify the current device's media characteristics and constraints.

## Disabling Animations

To disable animations in your Flutter app using `MediaQuery`, follow these steps:

1. Import the necessary packages:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/scheduler.dart';
```

2. Wrap your app widget with a `MediaQuery` widget and set `disableAnimations` property to true:

```dart
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MediaQuery(
      data: MediaQueryData.fromWindow(WidgetsBinding.instance.window)
          .copyWith(disableAnimations: true),
      child: MaterialApp(
        title: 'Disable Animations Demo',
        theme: ThemeData(
          primarySwatch: Colors.blue,
        ),
        home: MyHomePage(title: 'Disable Animations'),
      ),
    );
  }
}
```

3. Disable animations in the relevant parts of your app:

```dart
class MyHomePage extends StatelessWidget {
  MyHomePage({Key key, this.title}) : super(key: key);

  final String title;

  @override
  Widget build(BuildContext context) {
    // Disable animations for specific widgets
    return Scaffold(
      appBar: AppBar(
        title: Text(title),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text(
              'Disable Animations Demo',
              style: Theme.of(context).textTheme.headline4,
            ),
            const SizedBox(height: 16),
            const FlutterLogo(size: 100),
            const SizedBox(height: 16),
            Text(
              'Animations are disabled.',
              style: Theme.of(context).textTheme.subtitle1,
            ),
          ],
        ),
      ),
    );
  }
}
```

4. Run your Flutter app and you will see that animations are now disabled.

## Conclusion

When you want to disable animations in your Flutter app, the `MediaQuery` class offers a convenient way to achieve that. By setting the `disableAnimations` property to true, you can easily disable animations throughout your app. This can be useful for testing purposes or for creating a more streamlined user experience.

## Hashtags

#Flutter #Animations