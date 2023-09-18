---
layout: post
title: "Adding animations to ListView transitions in Flutter."
description: " "
date: 2023-09-15
tags: [animations]
comments: true
share: true
---

ListView transitions are a common feature in many Flutter applications, providing a smooth and engaging user experience. While ListView itself comes with default transitions, adding animations can make your app more visually appealing and interactive.

In this tutorial, we will learn how to add animations to ListView transitions in Flutter. We will use the `AnimatedList` widget, which allows us to animate the addition, removal, and reordering of items in a ListView.

## Step 1: Set up the project

Before we start adding animations, let's set up a basic Flutter project. Open your preferred IDE and create a new Flutter project with a blank template.

## Step 2: Import dependencies 

To use the `AnimatedList` widget, we need to import the `flutter` and `animations` packages in our `pubspec.yaml` file. Open the `pubspec.yaml` file, and under the `dependencies` section, add the following lines:

```yaml
dependencies:
  flutter:
    sdk: flutter
  animations: ^2.0.0
```

Save the file and run `flutter pub get` to download the dependencies.

## Step 3: Create the data model

Next, let's create a simple data model that represents the items in our ListView. In a new file called `list_item.dart`, add the following code:

```dart
class ListItem {
  final String title;
  
  ListItem(this.title);
}
```

## Step 4: Implement the ListView

Now, let's implement the ListView with animations. In your main.dart file, replace the default `MyHomePage` widget with the following code:

```dart
import 'package:flutter/material.dart';
import 'list_item.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'ListView Animations',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  final List<ListItem> _items = [];
  final GlobalKey<AnimatedListState> _listKey = GlobalKey<AnimatedListState>();

  @override
  void initState() {
    super.initState();
    // Add some initial items to the list
    _items.add(ListItem('Item 1'));
    _items.add(ListItem('Item 2'));
    _items.add(ListItem('Item 3'));
  }

  void _addItem() {
    final index = _items.length;
    
    // Insert the new item to the list
    _items.insert(index, ListItem('New Item'));

    // Animate the new item into the listView
    _listKey.currentState?.insertItem(index);
  }

  void _removeItem(int index) {
    final item = _items.removeAt(index);

    // Animate the removal of the item from the listView
    _listKey.currentState?.removeItem(
      index,
      (context, animation) => ListTile(
        title: Text(
          item.title,
          style: TextStyle(color: Colors.red),
        ),
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('ListView Animations'),
      ),
      body: AnimatedList(
        key: _listKey,
        initialItemCount: _items.length,
        itemBuilder: (context, index, animation) {
          return _buildItem(_items[index], animation);
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _addItem,
        child: Icon(Icons.add),
      ),
    );
  }

  Widget _buildItem(ListItem item, Animation<double> animation) {
    return SizeTransition(
      sizeFactor: animation,
      child: ListTile(
        title: Text(item.title),
        trailing: IconButton(
          icon: Icon(Icons.delete),
          onPressed: () => _removeItem(_items.indexOf(item)),
        ),
      ),
    );
  }
}
```

## Step 5: Run the app

Save the file and run the app on a simulator or physical device. You should see a ListView with some initial items. Tap the floating action button to add a new item, and swipe to delete an item. The animations will smoothly transition the items.

## Conclusion

In this tutorial, we learned how to add animations to ListView transitions in Flutter. We used the `AnimatedList` widget to achieve smooth and visually appealing transitions when adding and removing items from the list. Adding animations to your ListView transitions can greatly enhance the user experience of your Flutter app.

#flutter #animations