---
layout: post
title: "useDrawer hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: [flutterhooks, useDrawer]
comments: true
share: true
---

Flutter Hooks is a powerful package that provides a variety of hooks to make Flutter development more efficient and simpler. One of the hooks provided by Flutter Hooks is `useDrawer`, which allows you to easily manage the state and functionality of a drawer in your Flutter app.

To use the `useDrawer` hook in your app, follow the steps below:

1. Import the necessary packages:
```dart
import 'package:flutter/material.dart';
import 'package:flutter_hooks/flutter_hooks.dart';
```

2. Create a custom widget to represent your app:
```dart
class MyApp extends HookWidget {
  @override
  Widget build(BuildContext context) {
    final DrawerControllerState drawerController = useDrawerController();
    final isDrawerOpen = useState(false);

    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Flutter Hooks - useDrawer'),
        ),
        drawer: Drawer(
          child: ListView(
            padding: EdgeInsets.zero,
            children: [
              DrawerHeader(
                child: Text('Drawer Header'),
                decoration: BoxDecoration(
                  color: Colors.blue,
                ),
              ),
              ListTile(
                title: Text('Item 1'),
                onTap: () {
                  drawerController.close();
                  isDrawerOpen.value = false;
                },
              ),
              ListTile(
                title: Text('Item 2'),
                onTap: () {
                  drawerController.close();
                  isDrawerOpen.value = false;
                },
              ),
            ],
          ),
        ),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Text('Welcome to Flutter Hooks - useDrawer'),
              RaisedButton(
                child: Text('Open Drawer'),
                onPressed: () {
                  drawerController.open();
                  isDrawerOpen.value = true;
                },
              ),
              isDrawerOpen.value ? Text('Drawer is open') : Text('Drawer is closed'),
            ],
          ),
        ),
      ),
    );
  }
}
```

3. Run your app:
```dart
void main() {
  runApp(MyApp());
}
```

In the above example, we create a custom `MyApp` widget that uses the `HookWidget`. We create an instance of `DrawerControllerState` using the `useDrawerController` hook and a `useState` hook to manage the state of the drawer. 

The `Drawer` widget is provided with a `ListView` containing the drawer items. Each item has an `onTap` callback that closes the drawer and sets the drawer state to closed. The `RaisedButton` in the body opens the drawer and sets the state to open. The state of the drawer is then displayed dynamically using conditional rendering.

By using the `useDrawer` hook, managing the drawer state and functionality becomes much simpler and more streamlined in a Flutter app.

#flutter #flutterhooks #useDrawer