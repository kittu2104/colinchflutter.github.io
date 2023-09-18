---
layout: post
title: "Building expandable ListView items in Flutter."
description: " "
date: 2023-09-15
tags: [Widgets]
comments: true
share: true
---

In this tutorial, we will explore how to build expandable ListView items in Flutter, allowing users to expand and collapse the content within each item. This is a common user interface pattern that is useful for displaying hierarchical data or nested content.

## Step 1: Set up Flutter project
Before we begin, make sure you have Flutter installed on your machine. If not, you can [install Flutter here](https://flutter.dev/docs/get-started/install).

Create a new Flutter project using the following command:

```
flutter create expandable_listview
```

Change directory to the project folder:

```
cd expandable_listview
```

Open the project in your preferred code editor.

## Step 2: Create a ListView
In the `lib` folder, open the `main.dart` file.

Remove the default code and add the following code to create a basic ListView widget:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Expandable ListView'),
        ),
        body: ListView.builder(
          itemCount: 5,
          itemBuilder: (BuildContext context, int index) {
            return ListTile(
              title: Text('Item $index'),
            );
          },
        ),
      ),
    );
  }
}
```

This code sets up a simple ListView with 5 items displaying `Item 0`, `Item 1`, `Item 2`, `Item 3`, `Item 4`. However, the items are not yet expandable.

## Step 3: Make items expandable
To make the items expandable, we will use the `ExpansionTile` widget provided by Flutter.

Replace the `ListView.builder` widget with the following code:

```dart
ExpansionTile(
  title: Text('Item $index'),
  children: <Widget>[
    // Add additional content here
  ],
)
```

This will create an `ExpansionTile` for each item in the ListView. The `title` property sets the text displayed for each item.

Now we need to add some additional content inside each `ExpansionTile`. For example, let's add a subtitle and a button:

```dart
ExpansionTile(
  title: Text('Item $index'),
  subtitle: Text('Subtitle'),
  children: <Widget>[
    RaisedButton(
      child: Text('Expandable Content'),
      onPressed: () {
        // Add functionality here
      },
    ),
  ],
)
```

This code adds a subtitle to each item and a `RaisedButton` as the expandable content when the user taps on an item.

## Step 4: State management
To handle the expansion state of each item, we need to introduce state management.

Add a list of booleans to keep track of the expansion state for each item:

```dart
List<bool> _isExpandedList = List.generate(5, (index) => false);
```

Replace the `ExpansionTile` widget code with the following code:

```dart
ExpansionPanelList(
  expandedHeaderPadding: EdgeInsets.zero,
  elevation: 1,
  expansionCallback: (int index, bool isExpanded) {
    setState(() {
      _isExpandedList[index] = !isExpanded;
    });
  },
  children: <ExpansionPanel>[
    for (int i = 0; i < 5; i++)
      ExpansionPanel(
        headerBuilder: (BuildContext context, bool isExpanded) {
          return ListTile(
            title: Text('Item $i'),
          );
        },
        body: ListTile(
          title: Text('Subtitle'),
          trailing: RaisedButton(
            child: Text('Expandable Content'),
            onPressed: () {
              // Add functionality here
            },
          ),
        ),
        isExpanded: _isExpandedList[i],
      ),
  ],
)
```

This code uses the `ExpansionPanelList` widget to manage the expansion state of each item. The expansion state is controlled by the `_isExpandedList`. The `expansionCallback` is responsible for updating the state when an item is expanded or collapsed.

## Conclusion
Congratulations! You have successfully built expandable ListView items in Flutter. This pattern is useful for displaying hierarchical or nested content in an organized and user-friendly way. Feel free to customize the expandable content and add more interactivity according to your needs.

#Flutter #Widgets