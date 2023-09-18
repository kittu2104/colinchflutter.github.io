---
layout: post
title: "Implementing drag-and-drop functionality in ListView in Flutter."
description: " "
date: 2023-09-15
tags: [DragAndDrop]
comments: true
share: true
---

Drag-and-drop functionality can greatly enhance the user experience in your Flutter app. In this blog post, we will explore how to implement drag-and-drop functionality in a ListView widget.

## Prerequisites

Before getting started, make sure you have Flutter and Dart installed on your machine. Also, ensure that you have a basic understanding of Flutter widgets and state management.

## Adding Dependencies

To implement drag-and-drop functionality, we need to add the `flutter_reorderable_list` package to our project. Open your `pubspec.yaml` file and add the following line under the `dependencies` section:

```yaml
dependencies:
  flutter_reorderable_list: ^0.1.0
```

Save the file and run `flutter pub get` in your terminal to fetch the new dependency.

## Creating the ListView

Let's create a simple ListView widget that displays a list of items. In this example, we will use a `List<String>` to represent the data model. Replace the contents of your main.dart file with the following code:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    List<String> items = ['Item 1', 'Item 2', 'Item 3', 'Item 4'];

    return MaterialApp(
      title: 'Drag and Drop ListView',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Drag and Drop ListView'),
        ),
        body: ReorderableListView(
          onReorder: (int oldIndex, int newIndex) {
            // Handle reordering logic here
          },
          children: [
            for (final item in items)
              ListTile(
                key: ValueKey(item),
                title: Text(item),
              ),
          ],
        ),
      ),
    );
  }
}
```

## Implementing Drag-and-Drop

Now that we have our ListView set up, let's add the drag-and-drop functionality. In the `onReorder` callback, we can handle the logic to reorder the items in our data model. Modify the `onReorder` callback in the `ReorderableListView` as shown below:

```dart
onReorder: (int oldIndex, int newIndex) {
  // Handle reordering logic here
  if (newIndex > oldIndex) {
    newIndex -= 1;
  }
  final item = items.removeAt(oldIndex);
  items.insert(newIndex, item);
},
```

In this example, we remove the item from the old index and insert it at the new index. We also adjust the new index to consider the removal of the item.

## Customizing the Drag Handle

By default, the drag handle in the `ListTile` widget is the entire tile, which may not be visually appealing. You can customize the drag handle by wrapping the `ListTile` in a `Card` widget and adding a drag handle icon. 

```dart
children: [
  for (final item in items)
    Card(
      key: ValueKey(item),
      child: ListTile(
        leading: Icon(Icons.drag_handle),
        title: Text(item),
      ),
    ),
],
```

In the above code, we wrap the `ListTile` widget in a `Card` and add an `Icon` widget as the leading widget. This provides a visual indication of the drag handle.

## Conclusion

In this blog post, we learned how to implement drag-and-drop functionality in a ListView widget in Flutter. We added the `flutter_reorderable_list` dependency, created a ListView, and customized the drag handle. With this knowledge, you can now enhance your Flutter app's user experience by allowing users to easily reorder items in a list. Happy coding!

---
Tags: #Flutter #DragAndDrop