---
layout: post
title: "ListView with multiple selection support in Flutter."
description: " "
date: 2023-09-15
tags: [MultipleSelectionListView]
comments: true
share: true
---

In Flutter, the `ListView` widget provides a way to display a list of items. By default, `ListView` allows a single item to be selected at a time. However, there are cases where multiple selection support is required. In this blog post, we will explore how to implement a `ListView` with multiple selection support in Flutter.

## Step 1: Define the Model

First, we need to define a model class to represent each item in the list. Let's create a simple `Item` class with a `String` property called `name`:

```dart
class Item {
  String name;

  Item(this.name);
}
```

## Step 2: Create the ListView

Next, we can create a `ListView` and populate it with `Item` objects. Here's an example of how to create a basic `ListView` with multiple selection support:

```dart
class MultipleSelectionListView extends StatefulWidget {
  @override
  _MultipleSelectionListViewState createState() =>
      _MultipleSelectionListViewState();
}

class _MultipleSelectionListViewState extends State<MultipleSelectionListView> {
  List<Item> items = [
    Item('Item 1'),
    Item('Item 2'),
    Item('Item 3'),
    Item('Item 4'),
  ];

  List<bool> selectedItems = List.generate(4, (index) => false);

  @override
  Widget build(BuildContext context) {
    return ListView.builder(
      itemCount: items.length,
      itemBuilder: (BuildContext context, int index) {
        return ListTile(
          title: Text(items[index].name),
          leading: Checkbox(
            value: selectedItems[index],
            onChanged: (bool value) {
              setState(() {
                selectedItems[index] = value;
              });
            },
          ),
        );
      },
    );
  }
}
```

In the code above, we have a list of `Item` objects and a list of boolean values to keep track of the selected items. Each item is displayed using a `ListTile`, which contains a `Checkbox` to enable multiple selection. The `selectedItems` list is updated when the value of the `Checkbox` changes.

## Step 3: Getting Selected Items

To get a list of selected items, we can create a method in the `MultipleSelectionListView` class to iterate over the `selectedItems` list and return a list of selected `Item` objects:

```dart
List<Item> getSelectedItems() {
  List<Item> selectedItems = [];
  for (int i = 0; i < items.length; i++) {
    if (selectedItems[i]) {
      selectedItems.add(items[i]);
    }
  }
  return selectedItems;
}
```

## Conclusion

By following the steps above, you can implement a `ListView` with multiple selection support in Flutter. This can be useful in various scenarios where you need to allow users to select multiple items from a list. Feel free to customize the `ListView` layout and design to match the requirements of your app.

#Flutter #MultipleSelectionListView