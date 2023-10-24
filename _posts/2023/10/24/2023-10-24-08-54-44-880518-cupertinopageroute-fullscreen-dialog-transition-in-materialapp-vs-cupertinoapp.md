---
layout: post
title: "CupertinoPageRoute fullscreen dialog transition in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When developing mobile applications, it is essential to create smooth and intuitive transitions between different screens. One popular transition effect is the fullscreen dialog transition, which provides a seamless experience for users.

In Flutter, two commonly used widgets for building iOS-style applications are `MaterialApp` and `CupertinoApp`. These widgets provide different sets of UI components and follow different design guidelines. When it comes to implementing a fullscreen dialog transition, there are some differences to consider between these two widgets.

## 1. MaterialApp

`MaterialApp` is the widget used to create Material Design applications in Flutter. It provides a comprehensive set of UI components following the Material Design guidelines established by Google. To implement a fullscreen dialog transition in a `MaterialApp`, you can use the `MaterialPageRoute` class.

Here's an example of how to create a fullscreen dialog transition in `MaterialApp`:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    home: MyAppHomePage(),
    routes: {
      '/fullscreen_dialog': (context) => FullScreenDialogPage(),
    },
  ));
}

class MyAppHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Home'),
      ),
      body: Center(
        child: RaisedButton(
          child: Text('Open Fullscreen Dialog'),
          onPressed: () {
            Navigator.pushNamed(context, '/fullscreen_dialog');
          },
        ),
      ),
    );
  }
}

class FullScreenDialogPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Fullscreen Dialog'),
      ),
      body: Center(
        child: RaisedButton(
          child: Text('Close Dialog'),
          onPressed: () {
            Navigator.pop(context);
          },
        ),
      ),
    );
  }
}
```

In this example, we define two `Scaffold` widgets representing the home page and the fullscreen dialog. The `RaisedButton` widget in the `MyAppHomePage` triggers the navigation to the fullscreen dialog page using `Navigator.pushNamed`. The `RaisedButton` in the `FullScreenDialogPage` closes the dialog using `Navigator.pop`.

## 2. CupertinoApp

`CupertinoApp` is the widget used to create iOS-style applications in Flutter. It follows the specific design guidelines provided by Apple. To implement a fullscreen dialog transition in a `CupertinoApp`, we can use the `CupertinoPageRoute` class.

Here's an example of how to create a fullscreen dialog transition in `CupertinoApp`:

```dart
import 'package:flutter/cupertino.dart';

void main() {
  runApp(CupertinoApp(
    home: MyAppHomePage(),
    routes: {
      '/fullscreen_dialog': (context) => FullScreenDialogPage(),
    },
  ));
}

class MyAppHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(
        middle: Text('Home'),
      ),
      child: Center(
        child: CupertinoButton(
          child: Text('Open Fullscreen Dialog'),
          onPressed: () {
            Navigator.pushNamed(context, '/fullscreen_dialog');
          },
        ),
      ),
    );
  }
}

class FullScreenDialogPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(
        middle: Text('Fullscreen Dialog'),
      ),
      child: Center(
        child: CupertinoButton(
          child: Text('Close Dialog'),
          onPressed: () {
            Navigator.pop(context);
          },
        ),
      ),
    );
  }
}
```

In this example, we use `CupertinoPageScaffold` instead of `Scaffold` and `CupertinoButton` instead of `RaisedButton`. The rest of the code is similar to the previous example for `MaterialApp`.

## Conclusion

Both `MaterialApp` and `CupertinoApp` provide ways to implement a fullscreen dialog transition in Flutter. It is important to consider the design guidelines and UI components specific to each platform. By following the examples provided above, you can create a smooth transition experience for your users, whether you are building a Material Design or iOS-style application.

# References
- [Flutter MaterialApp](https://api.flutter.dev/flutter/material/MaterialApp-class.html)
- [Flutter CupertinoApp](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html)
- [Flutter MaterialPageRoute](https://api.flutter.dev/flutter/material/MaterialPageRoute-class.html)
- [Flutter CupertinoPageRoute](https://api.flutter.dev/flutter/cupertino/CupertinoPageRoute-class.html)