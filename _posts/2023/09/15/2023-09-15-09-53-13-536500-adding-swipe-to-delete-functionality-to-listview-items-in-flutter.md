---
layout: post
title: "Adding swipe-to-delete functionality to ListView items in Flutter."
description: " "
date: 2023-09-15
tags: [flutter]
comments: true
share: true
---

Flutter is a popular framework for building beautiful and fast user interfaces. When working with ListView widgets, it is often useful to add swipe-to-delete functionality to items in the list. In this blog post, we will explore how to achieve this in Flutter.

## Prerequisites

To follow along with this tutorial, make sure you have Flutter installed on your machine. You will also need a basic understanding of Flutter and Dart programming.

## Getting Started

First, create a new Flutter project by running the following command in your terminal:

```shell
flutter create swipe_to_delete
```

Navigate to the project directory:

```shell
cd swipe_to_delete
```

Open the `pubspec.yaml` file and add the `flutter_slidable` package as a dependency:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_slidable: ^1.1.0
```

Save the file and run the following command to fetch the package:

```shell
flutter pub get
```

## Implementing Swipe-to-Delete

Open the `lib/main.dart` file and replace the code with the following:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_slidable/flutter_slidable.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Swipe to Delete',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
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
  List<String> items = List.generate(10, (index) => 'Item $index');

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Swipe to Delete'),
      ),
      body: ListView.builder(
        itemCount: items.length,
        itemBuilder: (context, index) {
          final item = items[index];
          return Slidable(
            actionPane: SlidableDrawerActionPane(),
            actionExtentRatio: 0.25,
            child: ListTile(
              title: Text(item),
            ),
            actions: [
              IconSlideAction(
                caption: 'Delete',
                color: Colors.red,
                icon: Icons.delete,
                onTap: () {
                  setState(() {
                    items.removeAt(index);
                  });
                },
              ),
            ],
          );
        },
      ),
    );
  }
}
```

Save the file and run the app using the following command:

```shell
flutter run
```

Now you should see a list of items, each of which can be swiped to reveal a delete action. Tapping on the delete action will remove the corresponding item from the list.

## Summary

In this tutorial, we learned how to implement swipe-to-delete functionality in a ListView using the `flutter_slidable` package. By adding this feature to your app, you can enhance the user experience and make managing lists of items more intuitive.

Be sure to check out the official Flutter documentation for more information on working with ListView widgets and handling gestures.

#flutter #ui