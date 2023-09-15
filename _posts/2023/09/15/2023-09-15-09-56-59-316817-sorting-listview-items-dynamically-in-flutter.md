---
layout: post
title: "Sorting ListView items dynamically in Flutter."
description: " "
date: 2023-09-15
tags: [flutter, sorting]
comments: true
share: true
---
Flutter is a popular framework for building cross-platform apps. One common requirement in app development is to sort items in a ListView widget dynamically. In this blog post, we will discuss how to achieve this in Flutter.

## Adding sortable functionality to ListView
To make our ListView sortable, we will use the `ListView.builder` widget along with a list of data items. We will also introduce a sorting mechanism to rearrange the items based on a selected sorting criteria.

Let's start by setting up the basic structure of our app. Create a new Flutter project and replace the contents of `lib/main.dart` with the following code:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Sorting ListView',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  List<String> items = [
    'Item 1',
    'Item 2',
    'Item 3',
    'Item 4',
    'Item 5',
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Sorting ListView'),
      ),
      body: ListView.builder(
        itemCount: items.length,
        itemBuilder: (context, index) {
          return ListTile(
            title: Text(items[index]),
          );
        },
      ),
    );
  }
}
```

In this code, we have a simple `ListView.builder` widget displaying a list of items. Now let's add the sorting functionality.

## Adding sorting buttons
To add sorting buttons for our ListView, we will make use of the `AppBar` widget. Modify the `AppBar` code in `_MyHomePageState` as follows:

```dart
AppBar(
  title: Text('Sorting ListView'),
  actions: <Widget>[
    IconButton(
      icon: Icon(Icons.sort_by_alpha),
      onPressed: () {
        setState(() {
          items.sort();
        });
      },
    ),
    IconButton(
      icon: Icon(Icons.sort),
      onPressed: () {
        setState(() {
          items.shuffle();
        });
      },
    ),
  ],
)
```

In this code, we have added two `IconButton` widgets to the `actions` list of the `AppBar`. The first button sorts the items in ascending order, while the second button shuffles the items randomly. The sorting functionality is implemented using the `sort` and `shuffle` methods of the `List` class.

## Conclusion
By adding sorting buttons to our ListView and implementing the sorting logic, we have successfully achieved dynamic sorting of items in Flutter. This feature is useful in many scenarios, such as displaying a list of products in an e-commerce app or sorting a list of tasks in a to-do app.

Implementing dynamic sorting in a ListView allows users to interact with the app and manipulate the displayed data according to their preferences. This enhances the user experience and makes the app more versatile.

#flutter #sorting