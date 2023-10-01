---
layout: post
title: "useAppBarState hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: [flutter, flutterhooks]
comments: true
share: true
---

Flutter Hooks is a powerful library that provides an alternative to StatefulWidgets for managing state in Flutter applications. It offers a wide range of custom hooks that improve code organization and simplify state management.

In this blog post, we will explore the `useAppBarState` hook, which allows us to manage the state of an app bar in a Flutter application.

## Getting Started

To use the `useAppBarState` hook, we first need to add the `flutter_hooks` package to our project. Open your `pubspec.yaml` file and add the following line to the `dependencies` section:

```yaml
dependencies:
  flutter_hooks: ^0.18.0
```

After adding the package, run `flutter pub get` to install it.

## Implementing the UseAppBarState Hook

Now, let's see how we can use the `useAppBarState` hook in our Flutter application.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_hooks/flutter_hooks.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends HookWidget {
  @override
  Widget build(BuildContext context) {
    final appBarState = useAppBarState();
    
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Flutter Hooks Demo'),
        ),
        body: Column(
          children: [
            ElevatedButton(
              onPressed: appBarState.showAppBar,
              child: Text('Show AppBar'),
            ),
            ElevatedButton(
              onPressed: appBarState.hideAppBar,
              child: Text('Hide AppBar'),
            ),
          ],
        ),
      ),
    );
  }
}

AppBarState useAppBarState() {
  final showAppBar = useState(true);

  void _showAppBar() {
    showAppBar.value = true;
  }

  void _hideAppBar() {
    showAppBar.value = false;
  }

  return AppBarState(_showAppBar, _hideAppBar);
}

class AppBarState {
  final Function showAppBar;
  final Function hideAppBar;

  AppBarState(this.showAppBar, this.hideAppBar);
}
```

In the code snippet above, we defined a custom hook called `useAppBarState` that returns an `AppBarState` object. The `AppBarState` object contains two functions `showAppBar` and `hideAppBar` that update the state of the app bar.

Inside the `MyApp` widget, we call the `useAppBarState` hook to get access to the `appBarState`. We then use the `appBarState` to show or hide the app bar by invoking the `showAppBar` or `hideAppBar` functions, respectively.

## Conclusion

The `useAppBarState` hook is a handy utility provided by the Flutter Hooks library for managing the state of an app bar in Flutter applications. It simplifies the process of showing or hiding the app bar and improves code organization.

Using custom hooks like `useAppBarState` helps to make our codebase more readable, maintainable, and reusable. Flutter Hooks offers many other custom hooks for managing different aspects of state in Flutter applications.

Give the `useAppBarState` hook a try in your next Flutter project and experience the benefits of Flutter Hooks for yourself!

#flutter #flutterhooks