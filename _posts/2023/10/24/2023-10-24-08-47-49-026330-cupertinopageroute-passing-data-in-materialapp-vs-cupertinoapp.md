---
layout: post
title: "CupertinoPageRoute passing data in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [navigation]
comments: true
share: true
---

In building mobile applications, passing data between screens is a common requirement. Two popular frameworks for developing iOS applications with Flutter are `MaterialApp` and `CupertinoApp`. Both provide navigation capabilities and screen transitions. However, they differ in terms of the approach to passing data between screens.

## MaterialApp

`MaterialApp` is the standard Flutter widget for building Material Design applications. It offers a wide range of UI components and follows the Material Design guidelines. To pass data between screens with `MaterialApp`, you can use the `Navigator` widget and the `Navigator.push` method.

Here's an example of how to pass data using `MaterialApp`:

```dart
class ScreenA extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return RaisedButton(
      onPressed: () {
        Navigator.push(
          context,
          MaterialPageRoute(
            builder: (context) => ScreenB(data: 'Hello from Screen A'),
          ),
        );
      },
      child: Text('Go to Screen B'),
    );
  }
}

class ScreenB extends StatelessWidget {
  final String data;

  ScreenB({this.data});

  @override
  Widget build(BuildContext context) {
    return Text(data);
  }
}
```

In the example above, `ScreenA` contains a button that navigates to `ScreenB` when pressed. The `ScreenB` widget accepts the `data` parameter, which can be passed from `ScreenA` using the `Navigator.push` method with the `builder` parameter.

## CupertinoApp

`CupertinoApp` is another Flutter widget used for building iOS-style applications. It follows the Cupertino design guidelines, providing a sleek and modern interface. To pass data between screens with `CupertinoApp`, you can use the `CupertinoPageRoute` class and the `Navigator.push` method, similar to `MaterialApp`.

Here's an example of how to pass data using `CupertinoApp`:

```dart
class ScreenA extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return RaisedButton(
      onPressed: () {
        Navigator.push(
          context,
          CupertinoPageRoute(
            builder: (context) => ScreenB(data: 'Hello from Screen A'),
          ),
        );
      },
      child: Text('Go to Screen B'),
    );
  }
}

class ScreenB extends StatelessWidget {
  final String data;

  ScreenB({this.data});

  @override
  Widget build(BuildContext context) {
    return Text(data);
  }
}
```

In this example, the only difference is the usage of `CupertinoPageRoute` instead of `MaterialPageRoute`. The concept of passing data remains the same.

Both `MaterialApp` and `CupertinoApp` provide ways to pass data between screens, and the choice between the two depends on the design guidelines and UI components you want to follow for your application. Remember to import the necessary Flutter packages to use the respective navigation features.

---

**References:**
- [Flutter - MaterialApp class](https://api.flutter.dev/flutter/material/MaterialApp-class.html)
- [Flutter - CupertinoApp class](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html)
- [Flutter - Navigator class](https://api.flutter.dev/flutter/widgets/Navigator-class.html)
- [Flutter - CupertinoPageRoute class](https://api.flutter.dev/flutter/cupertino/CupertinoPageRoute-class.html)

---

#flutter #navigation