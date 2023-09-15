---
layout: post
title: "ListView with floating action button in Flutter."
description: " "
date: 2023-09-15
tags: [flutter, ListView, FloatingActionButton]
comments: true
share: true
---

In this blog post, we will discuss how to implement a `ListView` with a floating action button (FAB) in a Flutter application. The FAB is a commonly used UI element that provides quick access to primary actions. By combining it with a `ListView`, we can create a user-friendly interface to display a list of items.

To get started, let's create a new Flutter project and open the main.dart file. We will be working with the `Scaffold` widget, which provides a basic layout structure for the app. Inside the `Scaffold`, we will add a `FloatingActionButton` and a `ListView` widget.

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'ListView with FAB',
      home: Scaffold(
        appBar: AppBar(
          title: Text('ListView with FAB'),
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: () {},
          child: Icon(Icons.add),
        ),
        body: ListView.builder(
          itemCount: 10,
          itemBuilder: (context, index) {
            return ListTile(
              title: Text('Item $index'),
            );
          },
        ),
      ),
    );
  }
}
```

In the code above, we have a simple Flutter app with a `Scaffold` widget as the root. Inside the `Scaffold`, we have an `AppBar` with a title, a `FloatingActionButton` with an `onPressed` callback, and a `ListView.builder` which creates a list of 10 `ListTile` widgets.

You can customize the `ListView` by providing a different `itemCount` and adjusting the `itemBuilder` function to display the desired content for each item.

After saving and running the app, you will see a list of 10 items with an "Add" button floating above the `ListView`. You can now customize the `onPressed` callback of the FAB to perform any desired action, such as adding new items to the list.

By implementing a `ListView` with a floating action button, you can create a visually appealing and user-friendly UI in your Flutter app. This combination enables users to scroll through a list of items while also providing easy access to primary actions.

#flutter #ListView #FloatingActionButton