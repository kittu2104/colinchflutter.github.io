---
layout: post
title: "Implementing reordering functionality in ListView items in Flutter."
description: " "
date: 2023-09-15
tags: [flutter, reorderablelistview]
comments: true
share: true
---

Reordering functionality allows users to drag and reorder items in a ListView. In this blog post, we will explore how to implement this feature in Flutter, a popular cross-platform app development framework.

## Setting up the ListView

To get started, we need to set up a ListView with a list of items that can be reordered. Here's an example code snippet to create a basic ListView in Flutter:

```dart
ListView.builder(
  itemCount: items.length,
  itemBuilder: (context, index) {
    return ListTile(
      title: Text(items[index]),
    );
  },
)
```

In the `items` list, you can populate data that you want to display in the ListView.

## Adding reorder functionality

To enable reordering functionality, Flutter provides the `ReorderableListView` widget. This widget allows us to drag and reorder items within the ListView. Here's an example code snippet to add reordering functionality to our ListView:

```dart
ReorderableListView(
  children: List.generate(
    items.length,
    (index) {
      return ListTile(
        key: ValueKey(items[index]),
        title: Text(items[index]),
      );
    },
  ),
  onReorder: (oldIndex, newIndex) {
    setState(() {
      if (newIndex > oldIndex) {
        newIndex -= 1;
      }
      final item = items.removeAt(oldIndex);
      items.insert(newIndex, item);
    });
  },
)
```

In the above code, we wrap our `ListView` with the `ReorderableListView` widget. The `children` property takes a list of widgets, where each widget represents an item in the list. We use `List.generate` to generate `ListTile` widgets for each item.

The `key` property is set to a `ValueKey` with the value of the item. This is required for proper reordering.

The `onReorder` callback is triggered when an item is dragged and dropped to a new position. Inside the callback, we update the `items` list to reflect the new order of items.

## Customizing reordering behavior

The `ReorderableListView` widget allows customization of the reordering behavior through various properties:

- `header` and `footer`: These properties allow adding headers and footers to the ListView.
- `scrollDirection`: Specify the scrolling direction of the ListView.
- `physics`: Define the physics behavior of the ListView.
- `proxyDecorator`: Customize the appearance of the dragged item during reordering.

Check out the official Flutter documentation for more details on these properties and their usage.

## Conclusion

In this blog post, we have learned how to implement reordering functionality in ListView items in Flutter using the `ReorderableListView` widget. With this feature, your users can easily rearrange items in a list, providing a more interactive and intuitive user experience.

#flutter #reorderablelistview