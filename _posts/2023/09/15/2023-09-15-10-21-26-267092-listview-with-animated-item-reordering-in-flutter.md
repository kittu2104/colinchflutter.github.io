---
layout: post
title: "ListView with animated item reordering in Flutter."
description: " "
date: 2023-09-15
tags: [Flutter, ListReordering]
comments: true
share: true
---

In this blog post, we will explore how to implement a `ListView` with animated item reordering in Flutter. Reordering items in a list can be a common requirement in many applications, and adding animations to the reordering process can enhance the user experience.

## Prerequisites

Before we dive into the implementation, make sure you have a basic understanding of Flutter and have a Flutter development environment set up.

## Implementing Animated Item Reordering

To implement animated item reordering in a `ListView` in Flutter, we can make use of the `Draggable` and `LongPressDraggable` widgets along with `ReorderableListView`.

The `ReorderableListView` widget provides a built-in way to enable item reordering in a `ListView` by allowing users to long press and drag items. Here's an example of how we can use it:

```dart
ReorderableListView(
  children: List.generate(
    items.length,
    (index) => ListTile(
      key: Key('$index'),
      title: Text(items[index]),
    ),
  ),
  onReorder: (int oldIndex, int newIndex) {
    if (newIndex > oldIndex) {
      newIndex -= 1;
    }
    final item = items.removeAt(oldIndex);
    items.insert(newIndex, item);
  },
),
```

In the example above, we create a `ReorderableListView` and provide a list of `ListTile` widgets as its children. Each `ListTile` is given a unique key based on its index in the `items` list. The `onReorder` callback is called whenever an item is reordered, and updating the list accordingly.

To add animated transitions to the reordering process, we can wrap the `ListTile` with `Draggable` and `LongPressDraggable` widgets. Here's an enhanced example:

```dart
ReorderableListView(
  padding: EdgeInsets.symmetric(vertical: 8.0),
  children: List.generate(
    items.length,
    (index) => Draggable(
      key: Key('$index'),
      child: LongPressDraggable(
        child: ListTile(
          title: Text(items[index]),
        ),
      ),
      feedback: ListTile(
        title: Text(items[index]),
        **tileColor: Colors.grey,**  # Add a tile color to differentiate the dragged item.
        **selected: true,**  # Mark the tile as selected during dragging.
      ),
      childWhenDragging: Container(),  # Hide the original item during dragging.
    ),
  ),
  onReorder: (int oldIndex, int newIndex) {
    if (newIndex > oldIndex) {
      newIndex -= 1;
    }
    final item = items.removeAt(oldIndex);
    items.insert(newIndex, item);
  },
),
```

In this enhanced example, we wrap each `ListTile` with `Draggable` and `LongPressDraggable` widgets. We also provide feedback and a tile color to indicate the dragged item, mark the tile as selected during dragging, and hide the original item when it's being dragged.

## Conclusion

In this blog post, we learned how we can implement a `ListView` with animated item reordering in Flutter. By using the `ReorderableListView` widget and the `Draggable` and `LongPressDraggable` widgets, we can provide a seamless and visually pleasing reordering experience for the users of our Flutter applications.

Remember to experiment with different animations and visual effects to make your app stand out!

**#Flutter** **#ListReordering**