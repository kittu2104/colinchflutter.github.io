---
layout: post
title: "Using AnimatedList to create animated list items in Flutter."
description: " "
date: 2023-09-15
tags: [Flutter, AnimatedList]
comments: true
share: true
---

In Flutter, the `AnimatedList` widget allows you to create a list with animated transitions between the items. This can add a dynamic and visually appealing touch to your app's user interface.

Before diving into the code, make sure you have the Flutter SDK installed and a basic understanding of Flutter widgets and animations.

## Getting Started

To start using the `AnimatedList`, you need to first create an instance of `GlobalKey<AnimatedListState>` in your widget's state class. This allows you to access the methods of the `AnimatedList` widget.

```dart
GlobalKey<AnimatedListState> _listKey = GlobalKey<AnimatedListState>();
```

Next, you can create the `AnimatedList` widget and provide it with the necessary parameters.

```dart
AnimatedList(
  key: _listKey,
  initialItemCount: myItems.length,
  itemBuilder: (context, index, animation) {
    return _buildAnimatedListItem(myItems[index], animation);
  },
)
```

In this example, `myItems` is a list of items that you want to display in the animated list. The `initialItemCount` tells the `AnimatedList` the number of items it initially has.

You also need to define the `_buildAnimatedListItem` method, which takes an item and an animation, and returns the widget for that item.

```dart
Widget _buildAnimatedListItem(item, animation) {
  return SizeTransition(
    sizeFactor: animation,
    child: ListTile(
      title: Text(item.title),
      subtitle: Text(item.subtitle),
    ),
  );
}
```

The `SizeTransition` widget is used to animate the size of the list item. It takes the animation parameter and applies it to the `sizeFactor` property.

## Adding and Removing Items

To add or remove items from the `AnimatedList`, you can use the provided methods on the `AnimatedListState` obtained from the global key.

To add an item, use the `insertItem` method and provide the index at which to insert the item.

```dart
void addItem(Item item) {
  myItems.add(item);
  _listKey.currentState.insertItem(myItems.length - 1);
}
```

To remove an item, use the `removeItem` method and provide the index of the item to be removed.

```dart
void removeItem(int index) {
  _listKey.currentState.removeItem(index,
    (context, animation) => _buildAnimatedListItem(myItems[index], animation)
  );
  myItems.removeAt(index);
}
```

In the `removeItem` method, you also need to provide a callback that builds the widget for the item being removed.

## Conclusion

Using the `AnimatedList` widget in Flutter allows you to create an animated list with smooth transitions between the list items. You can easily add or remove items using the provided methods, giving your app a visually appealing and interactive user experience.

#Flutter #AnimatedList