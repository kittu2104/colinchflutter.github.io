---
layout: post
title: "useDrawerState hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: [flutter, flutterhooks]
comments: true
share: true
---

Managing the state of a drawer in Flutter can sometimes be a tedious task. However, with the use of Flutter Hooks, it becomes much simpler and more efficient. In this blog post, we will explore the `useDrawerState` hook provided by the Flutter Hooks library, and see how it can simplify your state management when working with drawers.

If you are not familiar with Flutter Hooks, it is a library that allows you to use stateful logic in a functional way, without the need for classes or StatefulWidget. It provides a set of hooks that you can leverage to manage different aspects of your Flutter app.

## The `useDrawerState` Hook

The `useDrawerState` hook is specifically designed to handle the state of a drawer. It manages the open and close actions of the drawer and provides a simple API to access and manipulate its state.

Here's an example of how you can use the `useDrawerState` hook in your Flutter app:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_hooks/flutter_hooks.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends HookWidget {
  @override
  Widget build(BuildContext context) {
    final drawerState = useDrawerState();

    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Flutter Hooks Drawer Example'),
        ),
        body: Center(
          child: Text('Welcome to Flutter Hooks!'),
        ),
        drawer: Drawer(
          child: ListView(
            padding: EdgeInsets.zero,
            children: <Widget>[
              ListTile(
                title: Text('Item 1'),
                onTap: () {
                  drawerState.close();
                },
              ),
              ListTile(
                title: Text('Item 2'),
                onTap: () {
                  drawerState.close();
                },
              ),
              ListTile(
                title: Text('Item 3'),
                onTap: () {
                  drawerState.close();
                },
              ),
            ],
          ),
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: () {
            drawerState.open();
          },
          child: Icon(Icons.menu),
        ),
      ),
    );
  }
}
```

In this example, we create a basic Flutter app with an app bar, a center-aligned text, and a floating action button. The `useDrawerState` hook is used to manage the state of the drawer. We open and close the drawer using the `open()` and `close()` methods provided by the `drawerState` object.

By using the `useDrawerState` hook, we eliminate the need for managing drawer state manually, making our code more readable and maintainable.

## Conclusion

The `useDrawerState` hook provided by Flutter Hooks simplifies the state management of a drawer in a Flutter app. It abstracts away the complexity of managing the state manually and provides a clean and efficient API to handle the open and close actions of the drawer.

By using the `useDrawerState` hook, you can make your code more readable and maintainable, allowing you to focus on building an awesome user interface.

#flutter #flutterhooks