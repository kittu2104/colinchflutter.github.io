---
layout: post
title: "Working with horizontal ListView in Flutter."
description: " "
date: 2023-09-15
tags: [listview]
comments: true
share: true
---

In this tutorial, I will show you how to work with a horizontal `ListView` in Flutter. The horizontal `ListView` allows you to display a scrolling list of items in a horizontal direction, making it ideal for displaying a list of images, products, or any other horizontally-scrollable content.

## Setting up the Project

Before we begin, make sure you have Flutter installed and set up on your machine. You can check the official Flutter documentation for installation instructions.

Create a new Flutter project by running the following command in your terminal:

```
flutter create horizontal_listview_example
```

Once the project is set up, navigate to the `lib` directory and open the `main.dart` file in your favorite code editor.

## Creating the Horizontal ListView

Replace the code in the `main.dart` file with the following code snippet:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Horizontal ListView Example',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Horizontal ListView Example'),
        ),
        body: HorizontalListView(),
      ),
    );
  }
}

class HorizontalListView extends StatelessWidget {
  final List<String> items = [
    'Item 1',
    'Item 2',
    'Item 3',
    'Item 4',
    'Item 5',
    'Item 6',
  ];

  @override
  Widget build(BuildContext context) {
    return ListView.builder(
      scrollDirection: Axis.horizontal,
      itemCount: items.length,
      itemBuilder: (context, index) {
        return Container(
          width: 120,
          margin: EdgeInsets.all(8),
          color: Colors.grey,
          child: Center(
            child: Text(
              items[index],
              style: TextStyle(
                fontSize: 16,
                fontWeight: FontWeight.bold,
              ),
            ),
          ),
        );
      },
    );
  }
}
```

In the code snippet above, we define a `HorizontalListView` widget that extends `StatelessWidget`. Inside the `build` method of the `HorizontalListView`, we use the `ListView.builder` widget to build a horizontal list of items.

## Running the App

Save the changes and run the app using the following command:

```
flutter run
```

Now you should be able to see the app running on the device or emulator. The app will display a horizontal list of items, each with a gray background and a text label.

## Conclusion

In this tutorial, we learned how to work with a horizontal `ListView` in Flutter. We created a simple horizontal list of items using the `ListView.builder` widget. You can customize the list by modifying the item widgets to fit your specific needs.

#flutter #listview