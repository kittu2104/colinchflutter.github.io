---
layout: post
title: "Implementing a swipe-to-archive with undo functionality in ListView in Flutter."
description: " "
date: 2023-09-15
tags: [ListView, SwipeToArchive, Undo]
comments: true
share: true
---

Swipe actions provide a convenient way to perform certain actions in a mobile app. In this tutorial, we will learn how to implement swipe-to-archive functionality in a ListView in Flutter. We will also incorporate an "undo" functionality to allow users to easily restore the archived item.

## Prerequisites

Make sure you have Flutter and the necessary dependencies set up. You should also have a basic understanding of Flutter concepts like Widgets and State management.

## Step 1: Set up the ListView

To begin, we need to set up a ListView to display the items that can be archived. We will use the `ListView.builder` constructor to build a dynamic list of items.

```dart
ListView.builder(
  itemCount: _items.length,
  itemBuilder: (BuildContext context, int index) {
    return ListTile(
      title: Text(_items[index]),
    );
  },
)
```

Here, `_items` is a list of strings that represents the item data we want to display in the list. You can replace it with your own data model.

## Step 2: Add swipe-to-archive functionality

To enable swipe actions, we will use the `Dismissible` widget provided by Flutter. Wrap the ListTile widget with `Dismissible` and provide the necessary parameters.

```dart
ListView.builder(
  itemCount: _items.length,
  itemBuilder: (BuildContext context, int index) {
    return Dismissible(
      key: Key(_items[index]),
      onDismissed: (direction) {
        setState(() {
          // Remove the item from the underlying data structure
          _items.removeAt(index);
        });

        ScaffoldMessenger.of(context).showSnackBar(
          SnackBar(content: Text("Item archived")),
        );
      },
      background: Container(
        color: Colors.red,
        child: Align(
          alignment: Alignment.centerRight,
          child: Padding(
            padding: EdgeInsets.only(right: 16.0),
            child: Icon(
              Icons.archive,
              color: Colors.white,
            ),
          ),
        ),
      ),
      child: ListTile(
        title: Text(_items[index]),
      ),
    );
  },
)
```

In the code above, we wrap the ListTile with `Dismissible`, provide a unique `key` for each item, and specify the `onDismissed` callback. In the `onDismissed` callback, we update the underlying data structure and display a snackbar to indicate that the item has been archived.

## Step 3: Add undo functionality

To add the undo functionality, we need to keep track of the item that was archived and provide a way to undo the action. Let's modify our code to achieve this.

```dart
ListView.builder(
  itemCount: _items.length,
  itemBuilder: (BuildContext context, int index) {
    String archivedItem;

    return Dismissible(
      key: Key(_items[index]),
      onDismissed: (direction) {
        setState(() {
          archivedItem = _items[index];
          _items.removeAt(index);
        });

        ScaffoldMessenger.of(context).showSnackBar(
          SnackBar(
            content: Text("Item archived"),
            action: SnackBarAction(
              label: "Undo",
              onPressed: () {
                setState(() {
                  _items.insert(index, archivedItem);
                });
              },
            ),
          ),
        );
      },
      // rest of the code...
    );
  },
)
```

In the modified code, we introduce a new variable `archivedItem` to store the archived item before removing it from the list. When the snackbar is shown, we provide an `action` that allows users to undo the archive action. On pressing the "Undo" button, we insert the archived item back into the list.

## Conclusion

By following the steps outlined in this tutorial, you have learned how to implement swipe-to-archive functionality with undo capability in a ListView in Flutter. This feature provides users with a seamless way to manage items in a mobile app. Use and customize this code as per your project requirements.

#flutter #ListView #SwipeToArchive #Undo