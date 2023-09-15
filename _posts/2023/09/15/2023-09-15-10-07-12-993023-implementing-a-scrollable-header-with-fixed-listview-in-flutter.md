---
layout: post
title: "Implementing a scrollable header with fixed ListView in Flutter."
description: " "
date: 2023-09-15
tags: []
comments: true
share: true
---

In this tutorial, we will learn how to create a scrollable header with a fixed ListView in Flutter. This type of layout is commonly used in applications where we want to display a header with some content that scrolls underneath it.

## Prerequisites

Before getting started, make sure you have Flutter installed on your machine. If not, you can follow the official Flutter installation guide for your operating system.

## Step 1 - Set up a new Flutter project

Create a new Flutter project by running the following command in your terminal:

```shell
flutter create scrollable_header_example
```

Once the project is created, navigate to the project directory:

```shell
cd scrollable_header_example
```

## Step 2 - Define the layout

Open the `lib/main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Scrollable Header Example',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: ScrollableHeaderPage(),
    );
  }
}

class ScrollableHeaderPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: CustomScrollView(
        slivers: [
          SliverAppBar(
            title: Text('Scrollable Header'),
            pinned: true,
            expandedHeight: 200,
            flexibleSpace: Placeholder(),
          ),
          SliverList(
            delegate: SliverChildBuilderDelegate(
              (BuildContext context, int index) {
                return ListTile(
                  title: Text('Item $index'),
                );
              },
              childCount: 20,
            ),
          ),
        ],
      ),
    );
  }
}
```

In the code above, we define a `CustomScrollView` widget that contains a `SliverAppBar` and a `SliverList`. The `SliverAppBar` displays the scrollable header with the title "Scrollable Header". We set `pinned` to `true` to keep the header fixed at the top of the screen. The `SliverList` contains a list of `ListTile` widgets as an example.

## Step 3 - Run the app

Save the changes and run the app using the following command:

```shell
flutter run
```

You should now see a screen with a scrollable header and a list of items underneath it. As you scroll the list, the header remains fixed at the top.

## Conclusion

In this tutorial, we learned how to implement a scrollable header with a fixed ListView in Flutter. This layout can be useful in various scenarios where we want to display important information at the top of the screen while allowing the content underneath to scroll.