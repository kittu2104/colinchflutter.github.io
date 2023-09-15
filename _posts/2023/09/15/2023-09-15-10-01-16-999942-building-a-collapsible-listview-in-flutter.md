---
layout: post
title: "Building a collapsible ListView in Flutter."
description: " "
date: 2023-09-15
tags: [flutter, collapsiblelistview]
comments: true
share: true
---

Flutter is a popular cross-platform framework for building high-performance mobile applications. One useful feature in many apps is the ability to have collapsible lists, where users can expand or collapse a section to view or hide its contents.

In this tutorial, we will walk through the process of building a collapsible ListView in Flutter using commonly used widgets such as `ListView.builder`, `ExpansionPanelList`, and `ExpansionPanel`. Let's get started!

## Step 1: Set Up Your Flutter Project

First, make sure you have Flutter installed on your machine. If not, follow the official Flutter installation guide for your operating system.

Next, create a new Flutter project using the Flutter CLI:

```
flutter create collapsible_listview
```

Navigate to the project directory:

```
cd collapsible_listview
```

Now, open the project in your favorite code editor. We are ready to start building our collapsible ListView.

## Step 2: Define the Model

For our example, let's assume we have a list of items with a title and description. We will create a model class to represent each item:

```dart
class ListItem {
  final String title;
  final String description;
  bool isExpanded;

  ListItem({required this.title, required this.description, this.isExpanded = false});
}
```

## Step 3: Create the UI

Now, open the `lib/main.dart` file and replace the default content with the following code:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(CollapsibleListViewApp());
}

class CollapsibleListViewApp extends StatelessWidget {
  final List<ListItem> items = [
    ListItem(title: 'Item 1', description: 'Description 1'),
    ListItem(title: 'Item 2', description: 'Description 2'),
    ListItem(title: 'Item 3', description: 'Description 3'),
  ];

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Collapsible ListView'),
        ),
        body: ListView.builder(
          itemCount: items.length,
          itemBuilder: (BuildContext context, int index) {
            return ExpansionPanelList(
              elevation: 1,
              expandedHeaderPadding: EdgeInsets.zero,
              expansionCallback: (int panelIndex, bool isExpanded) {
                setState(() {
                  items[index].isExpanded = !isExpanded;
                });
              },
              children: [
                ExpansionPanel(
                  headerBuilder: (BuildContext context, bool isExpanded) {
                    return ListTile(
                      title: Text(items[index].title),
                    );
                  },
                  body: ListTile(
                    title: Text(items[index].description),
                  ),
                  isExpanded: items[index].isExpanded,
                ),
              ],
            );
          },
        ),
      ),
    );
  }
}
```

In this code snippet, we define a `CollapsibleListViewApp` widget as the entry point for our app. Inside it, we declare a list of `ListItem` objects representing our data.

Then, we use the `ListView.builder` widget to render the list of items. Inside the builder, we wrap each item in an `ExpansionPanelList` widget, with an `ExpansionPanel` as its child.

We handle the expansion and collapsing of panels by updating the `isExpanded` property of each `ListItem` object in the `expansionCallback`. This updates the UI through the `setState` method.

## Step 4: Run the App

To run the app, use the following command:

```
flutter run
```

Now, you should see a collapsible ListView with the provided sample data. You can tap on the headers to expand or collapse the panels.

## Conclusion

In this tutorial, we learned how to build a collapsible ListView in Flutter using the `ExpansionPanelList` and `ExpansionPanel` widgets. You can now apply this knowledge to enhance the user experience in your Flutter apps by providing collapsible lists.

Remember to optimize your code by using appropriate data structures and widgets to handle large datasets efficiently. Enjoy building awesome Flutter apps!

#flutter #collapsiblelistview