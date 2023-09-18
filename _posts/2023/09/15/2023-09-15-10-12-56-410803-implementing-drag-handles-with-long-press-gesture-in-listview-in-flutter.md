---
layout: post
title: "Implementing drag handles with long press gesture in ListView in Flutter."
description: " "
date: 2023-09-15
tags: [draghandles, listview]
comments: true
share: true
---

Drag handles provide an intuitive way for users to rearrange items in a list. In Flutter, we can achieve this functionality using the `LongPressDraggable` widget along with a `ListView`. In this blog post, we will walk through the steps required to implement drag handles with a long press gesture in a `ListView` in Flutter.

## 1. Add dependencies

First, we need to add the necessary dependencies to our `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  draggable_scrollbar: ^0.1.4
```

The `draggable_scrollbar` package will help us in creating a draggable scrollbar for our `ListView`.

## 2. Create a ListView with drag handles

Next, let's create a simple `ListView` with drag handles. We can use the `LongPressDraggable` widget to wrap the list items and make them draggable. Add the following code to your Flutter project:

```dart
import 'package:flutter/material.dart';
import 'package:draggable_scrollbar/draggable_scrollbar.dart';

class DragHandlesListView extends StatefulWidget {
  @override
  _DragHandlesListViewState createState() => _DragHandlesListViewState();
}

class _DragHandlesListViewState extends State<DragHandlesListView> {
  final ScrollController _scrollController = ScrollController();

  List<String> _items = [
    'Item 1',
    'Item 2',
    'Item 3',
    'Item 4',
    'Item 5',
  ];

  @override
  Widget build(BuildContext context) {
    return DraggableScrollbar.rrect(
      controller: _scrollController,
      child: ListView.builder(
        controller: _scrollController,
        itemCount: _items.length,
        itemBuilder: (BuildContext context, int index) {
          return LongPressDraggable(
            feedback: Material(
              child: ListTile(
                title: Text(_items[index]),
                leading: Icon(Icons.drag_handle),
              ),
            ),
            childWhenDragging: Container(),
            data: index,
            child: ListTile(
              title: Text(_items[index]),
              leading: Icon(Icons.drag_handle),
            ),
          );
        },
      ),
    );
  }
}
```

In this code, we have created a stateful widget `DragHandlesListView`. Inside its build method, we have used `DraggableScrollbar.rrect` to add a draggable scrollbar around our `ListView`. The `DraggableScrollbar.rrect` widget requires a `controller` to be provided, so we have created a `ScrollController` to control the scroll position.

We have also used the `ListView.builder` widget to create our list. Inside the `itemBuilder` method, we wrap each item with `LongPressDraggable`. The `feedback` property of `LongPressDraggable` provides the visual representation of the dragged item. We have used a `Material` widget with `ListTile` to display the item with a drag handle icon. The `childWhenDragging` property is set to an empty container to hide the original item during dragging. Finally, the `data` property is set to the index of the item, which can be accessed when the item is dropped.

## 3. Implement onDragEnd callback

To rearrange the items when they are dropped, we need to implement the `onDragEnd` callback. Modify the `build` method in `_DragHandlesListViewState` as follows:

```dart
@override
Widget build(BuildContext context) {
  return DraggableScrollbar.rrect(
    controller: _scrollController,
    child: ListView.builder(
      controller: _scrollController,
      itemCount: _items.length,
      itemBuilder: (BuildContext context, int index) {
        return LongPressDraggable(
          feedback: Material(
            child: ListTile(
              title: Text(_items[index]),
              leading: Icon(Icons.drag_handle),
            ),
          ),
          childWhenDragging: Container(),
          data: index,
          child: ListTile(
            title: Text(_items[index]),
            leading: Icon(Icons.drag_handle),
          ),
          onDragEnd: (dragDetails) {
            setState(() {
              int fromIndex = dragDetails.data;
              int toIndex = _findInsertIndex(dragDetails.offset, index);
              if (fromIndex < toIndex) {
                toIndex -= 1;
              }
              String item = _items.removeAt(fromIndex);
              _items.insert(toIndex, item);
            });
          },
        );
      },
    ),
  );
}

int _findInsertIndex(Offset offset, int currentIndex) {
  RenderBox box = context.findRenderObject() as RenderBox;
  double y = box.globalToLocal(offset).dy;
  int index = currentIndex;
  if (y > 20) {
    index += 1;
  }
  return index;
}
```

In this code, we have added the `onDragEnd` callback to the `LongPressDraggable` widget. This callback is triggered when an item is dropped. Inside the `onDragEnd` callback, we calculate the `fromIndex` and `toIndex` of the dragged item. We use the `offset` (position) of the drag to determine the new index of the item. We also adjust the `toIndex` by subtracting 1 if the item is dropped below its initial position.

Finally, we remove the item from the `fromIndex` and insert it at the `toIndex` in the `_items` list. We wrap this operation inside `setState` to trigger a rebuild of the UI.

## Conclusion

By using `LongPressDraggable` along with a `ListView` in Flutter, we can easily implement drag handles with a long press gesture. The `LongPressDraggable` widget provides the necessary functionality to make items draggable, and the `ListView` allows us to display the list of items. With a few additional tweaks to handle the drag and drop operations, we can create a seamless and intuitive user experience.

#flutter #draghandles #listview