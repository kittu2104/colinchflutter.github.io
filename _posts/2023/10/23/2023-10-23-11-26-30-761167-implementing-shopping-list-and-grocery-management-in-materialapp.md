---
layout: post
title: "Implementing shopping list and grocery management in MaterialApp."
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

In this blog post, we will explore how to implement a shopping list and grocery management feature using the `MaterialApp` component in Flutter. Flutter is a popular cross-platform mobile app development framework developed by Google.

## Table of Contents

- [Introduction](#introduction)
- [Setting up the Project](#setting-up-the-project)
- [Creating the Shopping List Screen](#creating-the-shopping-list-screen)
- [Managing Groceries](#managing-groceries)
- [Conclusion](#conclusion)

## Introduction

Managing groceries and creating a shopping list is an essential task for many people. With the help of Flutter's `MaterialApp`, we can easily create an interactive and visually appealing shopping list and grocery management system.

## Setting up the Project

To get started, create a new Flutter project using your preferred IDE or the command line. This can be done by running the command `flutter create shopping_list_app`.

Next, open the project in your IDE and make sure to have the latest version of Flutter and Dart SDK installed.

## Creating the Shopping List Screen

To create the shopping list screen, we will make use of the `Scaffold` widget provided by `MaterialApp`. 

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(ShoppingListApp());
}

class ShoppingListApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Shopping List App',
      theme: ThemeData(primarySwatch: Colors.blue),
      home: ShoppingListScreen(),
    );
  }
}

class ShoppingListScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Shopping List'),
      ),
      body: ListView.builder(
        itemCount: 10,
        itemBuilder: (context, index) {
          return ListTile(
            title: Text('Item $index'),
          );
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          // Add new item to the shopping list
        },
        child: Icon(Icons.add),
      ),
    );
  }
}
```

In the above code, we have defined the `ShoppingListApp` which extends the `MaterialApp` component. The `ShoppingListScreen` widget represents the main shopping list screen. We have set up a basic `Scaffold` with an `AppBar` and a `ListView.builder` to display a list of items. We have also added a floating action button to allow users to add new items to the shopping list.

## Managing Groceries

To manage groceries, we will need to create a data model and implement functionality to add, update, and delete items from the shopping list. 

```dart
class Grocery {
  final String name;
  final bool isChecked;

  Grocery({required this.name, required this.isChecked});
}

class ShoppingListScreen extends StatefulWidget {
  @override
  _ShoppingListScreenState createState() => _ShoppingListScreenState();
}

class _ShoppingListScreenState extends State<ShoppingListScreen> {
  List<Grocery> groceries = [];

  void addItem(String name) {
    setState(() {
      groceries.add(Grocery(name: name, isChecked: false));
    });
  }

  void removeItem(int index) {
    setState(() {
      groceries.removeAt(index);
    });
  }

  void toggleItem(int index) {
    setState(() {
      groceries[index].isChecked = !groceries[index].isChecked;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      ...
    );
  }
}
```

In the above code, we have created a `Grocery` class to represent individual grocery items. The `ShoppingListScreen` widget is now a stateful widget to manage the list of groceries. We have implemented methods to add, remove, and toggle the checkboxes for groceries.

We can now update the `ListView.builder` to display the grocery items and handle the related functionality.

## Conclusion

With the help of `MaterialApp` and Flutter's powerful widget system, we can easily implement a shopping list and grocery management system. The code snippets provided in this blog post serve as a starting point for creating an interactive and visually appealing shopping list app. Feel free to explore and enhance the functionality as per your requirements.

Happy coding!

# References

1. [Flutter Documentation](https://flutter.dev/docs)
2. [MaterialApp class documentation](https://api.flutter.dev/flutter/material/MaterialApp-class.html)
3. [Scaffold class documentation](https://api.flutter.dev/flutter/material/Scaffold-class.html)