---
layout: post
title: "ListView with animated item insertion in Flutter."
description: " "
date: 2023-09-15
tags: []
comments: true
share: true
---

Flutter gives developers a wide variety of tools to create stunning user interfaces. One common UI element is a ListView, which allows for efficient scrolling of a list of items. In this tutorial, we'll learn how to create a ListView with animated item insertion in Flutter.

## Prerequisites

To follow this tutorial, you'll need to have Flutter installed on your machine. If you haven't already, head over to the Flutter website and follow their installation instructions.

## Setting up the Project

Let's start by creating a new Flutter project. Open your favorite text editor or IDE and create a new Flutter project with the following command:

```dart
$ flutter create animated_listview
```

## Implementing the Animated ListView

Inside the generated `lib` folder, open the `main.dart` file. We'll begin by setting up the basic structure of our app.

First, import the necessary packages:

```dart
import 'package:flutter/material.dart';
```

Next, create a new Flutter widget called `AnimatedListViewApp`:

```dart
void main() {
  runApp(AnimatedListViewApp());
}

class AnimatedListViewApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: AnimatedListView(),
    );
  }
}
```

Inside the `AnimatedListView` widget, we'll define a list of items and a function to add new items to the list:

```dart
List<int> items = [];
int nextItem = 1;

void addItem() {
  items.add(nextItem);
  nextItem++;
}
```

Now, let's create the `AnimatedListView` widget itself:

```dart
class AnimatedListView extends StatefulWidget {
  @override
  _AnimatedListViewState createState() => _AnimatedListViewState();
}

class _AnimatedListViewState extends State<AnimatedListView> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Animated ListView'),
      ),
      body: ListView.builder(
        itemCount: items.length,
        itemBuilder: (context, index) {
          return ListTile(
            title: Text('Item ${items[index]}'),
          );
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          setState(() {
            addItem();
          });
        },
        child: Icon(Icons.add),
      ),
    );
  }
}
```

In the `build` method of the `_AnimatedListViewState` class, we create a `ListView.builder` widget to display the list of items. We also add a `FloatingActionButton` at the bottom right corner to trigger the `addItem` function and update the state of the widget.

Finally, in the `main` function, we run the `AnimatedListViewApp`:

```dart
void main() {
  runApp(AnimatedListViewApp());
}
```

## Adding Animation

To animate the item insertion, we'll use the `AnimatedList` widget provided by Flutter. Edit the `AnimatedListView` widget as follows:

```dart
class _AnimatedListViewState extends State<AnimatedListView> {
  // declare animated list
  final GlobalKey<AnimatedListState> _listKey = GlobalKey<AnimatedListState>();
  
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Animated ListView'),
      ),
      body: AnimatedList(
        key: _listKey,
        initialItemCount: items.length,
        itemBuilder: (context, index, animation) {
          return SlideTransition(
            position: animation.drive(Tween(
              begin: Offset(-1, 0),
              end: Offset(0, 0),
            )),
            child: ListTile(
              title: Text('Item ${items[index]}'),
            ),
          );
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          setState(() {
            _listKey.currentState!.insertItem(items.length, duration: Duration(milliseconds: 500));
            addItem();
          });
        },
        child: Icon(Icons.add),
      ),
    );
  }
}
```

In this updated code, we have replaced the `ListView.builder` with an `AnimatedList`. We also added a `SlideTransition` to animate the item insertion. The `animation` argument in the `itemBuilder` provides the necessary animation information.

Inside the `onPressed` function of the `FloatingActionButton`, we call `insertItem` on the `_listKey.currentState` to insert a new item at the end of the list with a duration of 500 milliseconds. After inserting the item, we call the `addItem` function to increment the `nextItem` variable.

## Conclusion

Congratulations! You have successfully created a ListView with animated item insertion in Flutter. This can greatly enhance the user experience by providing smooth animations when adding items to a list. Feel free to customize the animation or add additional features to suit your app's needs.

Remember to use the `flutter` and `flutterdev` hashtags when sharing your code and experiences on social media. Happy coding!