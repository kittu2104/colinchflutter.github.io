---
layout: post
title: "Implementing a horizontally scrollable ListView in Flutter."
description: " "
date: 2023-09-15
tags: [listview]
comments: true
share: true
---

As a Flutter developer, you may come across situations where you need to display a list of items horizontally instead of vertically. In such cases, a horizontally scrollable ListView comes in handy. In this tutorial, we'll explore how to implement a horizontally scrollable ListView in Flutter.

## Prerequisites

Before getting started, make sure you have Flutter installed on your machine. You can follow the official [Flutter installation guide](https://flutter.dev/docs/get-started/install) for detailed instructions.

## Step 1: Create a Flutter project

To begin, create a new Flutter project by running the following command:

```
flutter create horizontal_listview
```

Navigate to the project folder:

```
cd horizontal_listview
```

Open the project in your preferred IDE or text editor.

## Step 2: Define the horizontal ListView

Open the `lib/main.dart` file and replace the default code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(HorizontalListViewApp());
}

class HorizontalListViewApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Horizontal ListView Example',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Horizontal ListView'),
        ),
        body: Center(
          child: Container(
            height: 200,
            child: ListView.builder(
              scrollDirection: Axis.horizontal,
              itemCount: 10,
              itemBuilder: (context, index) {
                return Container(
                  width: 150,
                  margin: EdgeInsets.only(right: 10),
                  color: Colors.grey.withOpacity(0.3),
                  child: Center(
                    child: Text(
                      'Item $index',
                      style: TextStyle(fontSize: 24),
                    ),
                  ),
                );
              },
            ),
          ),
        ),
      ),
    );
  }
}
```

## Step 3: Run the app

Save the changes and run the app on a simulator or physical device using the following command:

```
flutter run
```

You should see a horizontally scrollable ListView with 10 items, each with a gray background and displaying the item index.

## Conclusion

In this tutorial, we learned how to implement a horizontally scrollable ListView in Flutter. Using the `ListView.builder` widget with the `scrollDirection` property set to `Axis.horizontal`, we were able to achieve the desired effect. Remember to adapt the code to fit your specific use case.

#flutter #listview