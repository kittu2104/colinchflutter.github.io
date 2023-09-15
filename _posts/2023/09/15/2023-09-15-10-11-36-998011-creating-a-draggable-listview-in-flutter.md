---
layout: post
title: "Creating a draggable ListView in Flutter."
description: " "
date: 2023-09-15
tags: [Flutter, DraggableListView]
comments: true
share: true
---

In Flutter, ListView is a powerful widget for displaying a list of items. However, by default, ListView does not support the ability to drag and reorder its items. In this blog post, we will explore how to create a draggable ListView in Flutter, allowing users to rearrange items effortlessly.

## Getting Started

First, make sure you have Flutter installed on your machine. If not, you can follow the installation instructions on the official Flutter website.

## Adding Dependencies

To implement a draggable ListView, we need to add the `flutter_reorderable_list` package to our Flutter project. Open your `pubspec.yaml` file and add the following line to the `dependencies` section:

```yaml
dependencies:
  flutter_reorderable_list: ^0.2.1
```

Then, run the following command in your terminal to fetch the packages:

```
flutter pub get
```

## Implementing the Draggable ListView

In your Flutter project, create a new file named `draggable_list_view.dart` (or any other suitable name). Add the following code to the file:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_reorderable_list/flutter_reorderable_list.dart';

class DraggableListView extends StatefulWidget {
  @override
  _DraggableListViewState createState() => _DraggableListViewState();
}

class _DraggableListViewState extends State<DraggableListView> {
  List<String> items = ['Item 1', 'Item 2', 'Item 3', 'Item 4', 'Item 5'];

  @override
  Widget build(BuildContext context) {
    return ReorderableList(
      onReorder: _reorderCallback,
      child: ListView.builder(
        itemCount: items.length,
        itemBuilder: (context, index) {
          return ListTile(
            key: ValueKey(items[index]),
            title: Text(items[index]),
          );
        },
      ),
    );
  }

  void _reorderCallback(int oldIndex, int newIndex) {
    setState(() {
      if (oldIndex < newIndex) {
        newIndex -= 1;
      }
      final item = items.removeAt(oldIndex);
      items.insert(newIndex, item);
    });
  }
}
```

In this code, we have a `DraggableListView` widget that holds a list of items. We use the `ReorderableList` widget from the `flutter_reorderable_list` package to enable dragging and reordering functionality. The `ListView.builder` widget is used to display the items as a list of `ListTile` widgets.

Inside the `_reorderCallback` function, we handle the reordering logic by removing the item from the old index and inserting it at the new index.

## Integrating the Draggable ListView

To integrate the `DraggableListView` into your app, you can add it as a child widget in any other screen or scaffold. For example, in your `main.dart` file, modify the `MyApp` widget as follows:

```dart
import 'package:flutter/material.dart';
import 'draggable_list_view.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Draggable ListView Example',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Draggable ListView'),
        ),
        body: DraggableListView(),
      ),
    );
  }
}
```

Now, when you run your Flutter app, you should see a screen with a draggable ListView displaying the items "Item 1" to "Item 5". You can drag and reorder the items to change their positions.

## Conclusion

In this blog post, we have learned how to create a draggable ListView in Flutter using the `flutter_reorderable_list` package. This allows users to rearrange the items in the ListView by simply dragging them. By following these steps, you can now bring drag and reorder functionality to your Flutter app effortlessly.

#Flutter #DraggableListView