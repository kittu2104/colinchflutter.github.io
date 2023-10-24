---
layout: post
title: "CupertinoPageRoute transition curve in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [common]
comments: true
share: true
---

When building a Flutter application, you have the option to choose between `MaterialApp` and `CupertinoApp` as the root widget for your UI. Each of these widgets provides a different set of default styles and behaviors based on the targeted platform (Android or iOS). One noticeable difference between them is the transition curve used by the `PageRoute` when navigating between screens.

### MaterialApp

When using `MaterialApp`, the default transition curve for `PageRoute` is a gradual fade-in and fade-out effect. This means that as you navigate from one screen to another, the new screen will fade in gradually, while the old screen fades out. The effect is smooth and suits the Material Design guidelines for Android apps.

Here's an example code snippet that illustrates the usage of `MaterialApp`:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    home: MyAppHome(),
  ));
}

class MyAppHome extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('MaterialApp Transition')),
      body: Center(
        child: RaisedButton(
          child: Text('Go to another screen'),
          onPressed: () {
            Navigator.push(
              context,
              MaterialPageRoute(builder: (context) => SecondScreen()),
            );
          },
        ),
      ),
    );
  }
}

class SecondScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Second Screen')),
      body: Center(
        child: RaisedButton(
          child: Text('Go back'),
          onPressed: () {
            Navigator.pop(context);
          },
        ),
      ),
    );
  }
}
```

### CupertinoApp

On the other hand, when using `CupertinoApp`, the default transition curve for `PageRoute` is a slide-in and slide-out effect. This means that as you navigate from one screen to another, the new screen slides in from the right, while the old screen slides out to the left. This effect aligns with the visual style commonly found in iOS apps.

Here's an example code snippet that illustrates the usage of `CupertinoApp`:

```dart
import 'package:flutter/cupertino.dart';

void main() {
  runApp(CupertinoApp(
    home: MyAppHome(),
  ));
}

class MyAppHome extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(middle: Text('CupertinoApp Transition')),
      child: Center(
        child: RaisedButton(
          child: Text('Go to another screen'),
          onPressed: () {
            Navigator.push(
              context,
              CupertinoPageRoute(builder: (context) => SecondScreen()),
            );
          },
        ),
      ),
    );
  }
}

class SecondScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(middle: Text('Second Screen')),
      child: Center(
        child: RaisedButton(
          child: Text('Go back'),
          onPressed: () {
            Navigator.pop(context);
          },
        ),
      ),
    );
  }
}
```

As you can see, the most significant difference between the two code snippets is the widget imports and the widget hierarchy used. While `MaterialApp` uses `Scaffold`, `AppBar`, and `PageRoute`, `CupertinoApp` utilizes `CupertinoPageScaffold` and `CupertinoNavigationBar` along with `CupertinoPageRoute` for navigation.

While these examples help illustrate the different transition curves, it's important to note that both `MaterialApp` and `CupertinoApp` allow you to customize the transition behavior if the default curves do not fit your requirements. By providing your own custom `PageRouteBuilder`, you can define different animations, curves, and completion callbacks for navigating between screens.

In conclusion, when building a Flutter app, choosing between `MaterialApp` and `CupertinoApp` impacts not only the overall visual style but also the transition curve used when navigating between screens. Understanding these differences will help you create a cohesive and platform-specific user experience.

### References:
- [MaterialApp class - Flutter API documentation](https://api.flutter.dev/flutter/material/MaterialApp-class.html)
- [CupertinoApp class - Flutter API documentation](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html)
- [PageRoute class - Flutter API documentation](https://api.flutter.dev/flutter/widgets/PageRoute-class.html)
- [Material Design guidelines - Animation and Transitions](https://material.io/design/motion/the-motion-system.html#common-structural-transitions)  
- [Cupertino Design guidelines - Navigation and transitions](https://developer.apple.com/design/human-interface-guidelines/ios/app-architecture/navigation/)
- Flutter in Action (By Eric Windmill)