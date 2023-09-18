---
layout: post
title: "ListView with swipeable actions for each item in Flutter."
description: " "
date: 2023-09-15
tags: [swipeableListView]
comments: true
share: true
---

In many mobile applications, it is common to have a list of items where you can perform swipe actions on each item. Swipeable actions can provide users with quick and convenient ways to interact with the items in the list. In this blog post, we will explore how to implement a ListView with swipeable actions in Flutter.

## Setting up the Project

To get started, create a new Flutter project and set up the necessary dependencies. Open your project in your favorite code editor and navigate to the `pubspec.yaml` file. Add the following dependencies under the `dependencies` section:

```yaml
dependencies:
  flutter:
    sdk: flutter
  swipeable_item:
```

Save the file and run `flutter packages get` to fetch the required packages.

## Implementing the ListView

To implement a ListView with swipeable actions, we will be using the `SwipeableItem` package. Let's create a new Flutter widget called `SwipeableListView` and import the necessary packages:

```dart
import 'package:flutter/material.dart';
import 'package:swipeable_item/swipeable_item.dart';
```

Next, define a list of items that you want to display in the ListView:

```dart
final List<String> items = [
  'Item 1',
  'Item 2',
  'Item 3',
  'Item 4',
];
```

Inside the `build` method of the `SwipeableListView` widget, create a ListView.builder and wrap each item with the `SwipeableItem` widget:

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: Text('Swipeable ListView'),
    ),
    body: ListView.builder(
      itemCount: items.length,
      itemBuilder: (context, index) {
        final item = items[index];
        return SwipeableItem(
          key: Key(item),
          child: ListTile(
            title: Text(item),
          ),
          actions: [
            SwipeAction(
              color: Colors.red,
              icon: Icons.delete,
              onTap: () => _onSwipeActionTapped('Delete', item),
            ),
            SwipeAction(
              color: Colors.green,
              icon: Icons.archive,
              onTap: () => _onSwipeActionTapped('Archive', item),
            ),
          ],
        );
      },
    ),
  );
}
```

Here we are using the `SwipeAction` widget to define the swipe actions. Each action is associated with a color, an icon, and an `onTap` callback, which will be triggered when the user performs the associated action. The `_onSwipeActionTapped` method can be defined to perform the desired action when the user taps on a swipe action.

Finally, we need to define the `_onSwipeActionTapped` method:

```dart
void _onSwipeActionTapped(String action, String item) {
  showDialog(
    context: context,
    builder: (context) {
      return AlertDialog(
        title: Text('Action: $action'),
        content: Text('Item: $item'),
        actions: [
          FlatButton(
            child: Text('OK'),
            onPressed: () => Navigator.pop(context),
          ),
        ],
      );
    },
  );
}
```

This method displays an AlertDialog to show the action and the corresponding item when a swipe action is tapped.

## Testing the Swipeable ListView
Save all the changes and run your Flutter project with `flutter run`. You should see a ListView with swipeable actions for each item. Swipe left or right on an item to reveal the actions. Tap on the actions to see the corresponding dialogs displaying the action and item details.

## Conclusion
By using the `SwipeableItem` package, implementing a ListView with swipeable actions in Flutter becomes a straightforward process. You can now enhance the user experience by adding quick and intuitive swipe gestures to your list of items in your mobile applications.

#flutter #swipeableListView