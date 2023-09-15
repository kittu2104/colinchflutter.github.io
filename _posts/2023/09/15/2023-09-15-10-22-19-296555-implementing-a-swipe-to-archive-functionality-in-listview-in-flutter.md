---
layout: post
title: "Implementing a swipe-to-archive functionality in ListView in Flutter."
description: " "
date: 2023-09-15
tags: [flutter, swipeToArchive]
comments: true
share: true
---

In this tutorial, we will explore how to implement a swipe-to-archive functionality in a ListView widget using Flutter. This feature is commonly seen in email clients and to-do list applications, where users can swipe a list item to quickly archive it.

## Prerequisites
Before we begin, make sure you have Flutter and Dart installed on your machine. You can find the installation instructions in the Flutter documentation.

## Step 1: Set up a new Flutter project
Create a new Flutter project using the following command:

```dart
flutter create swipe_to_archive
```

## Step 2: Set up the ListView
Open the `lib/main.dart` file and replace its contents with the following code:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Swipe to Archive',
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
  final List<String> items = List.generate(20, (index) => 'Item ${index + 1}');

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Swipe to Archive'),
      ),
      body: ListView.builder(
        itemCount: items.length,
        itemBuilder: (context, index) => Dismissible(
          key: Key(items[index]),
          background: Container(
            color: Colors.red,
          ),
          direction: DismissDirection.endToStart,
          onDismissed: (direction) {
            setState(() {
              items.removeAt(index);
            });
          },
          child: ListTile(
            title: Text(items[index]),
          ),
        ),
      ),
    );
  }
}
```

In this code, we create a simple ListView with 20 items. Each item is wrapped in a `Dismissible` widget, which allows us to swipe it away for archiving. The `Dismissible` widget requires a unique key for each item, so we use the item's string value as the key.

The `background` property of `Dismissible` specifies the background color when the item is swiped. We set it to red in this example.

The `direction` property specifies the direction in which the item can be dismissed. Setting it to `endToStart` enables swiping from right to left (in an LTR layout).

The `onDismissed` callback is triggered when the item is dismissed. In this example, we remove the item from the list.

## Step 3: Run the app
Save the changes and run the app using the following command:

```dart
flutter run
```

You should now see a list of items that can be swiped to archive.

## Conclusion
Implementing a swipe-to-archive functionality in a ListView in Flutter is quite straightforward. By using the `Dismissible` widget and handling its `onDismissed` callback, we can easily add this feature to our app.

#flutter #swipeToArchive