---
layout: post
title: "Creating a searchable ListView in Flutter."
description: " "
date: 2023-09-15
tags: [flutter, searchableListView]
comments: true
share: true
---

Flutter is a powerful framework for building cross-platform apps, and one common requirement is to have a ListView that can be searched to find specific items. In this blog post, we will learn how to implement a searchable ListView in Flutter.

## Prerequisites
- Basic knowledge of Flutter and Dart programming language.

## Step 1: Setting up the project
1. Create a new Flutter project using `flutter create searchable_listview`.
2. Open the project in your favorite code editor.

## Step 2: Adding dependencies
1. Open the `pubspec.yaml` file in your project.
2. Add the following dependencies:
```markdown
dependencies:
  flutter:
    sdk: flutter
  cupertino_icons: ^1.0.2
```
3. Save the file and run `flutter pub get` to fetch the required dependencies.

## Step 3: Designing the UI
1. Open the `lib/main.dart` file in your project.
2. Replace the existing code with the following:
```dart
import 'package:flutter/material.dart';

void main() {
  runApp(SearchableListView());
}

class SearchableListView extends StatefulWidget {
  @override
  _SearchableListViewState createState() => _SearchableListViewState();
}

class _SearchableListViewState extends State<SearchableListView> {
  List<String> items = [
    'Item 1',
    'Item 2',
    'Item 3',
    'Item 4',
    'Item 5',
  ];

  List<String> filteredItems = [];

  @override
  void initState() {
    filteredItems.addAll(items);
    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Searchable ListView'),
        ),
        body: Column(
          children: [
            Padding(
              padding: const EdgeInsets.all(8.0),
              child: TextField(
                onChanged: (value) {
                  setState(() {
                    filteredItems = items
                        .where((item) =>
                            item.toLowerCase().contains(value.toLowerCase()))
                        .toList();
                  });
                },
                decoration: InputDecoration(
                  labelText: 'Search',
                ),
              ),
            ),
            Expanded(
              child: ListView.builder(
                itemCount: filteredItems.length,
                itemBuilder: (context, index) {
                  return ListTile(
                    title: Text(filteredItems[index]),
                  );
                },
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

## Step 4: Running the app
1. Save the file and run the app using `flutter run` command.
2. You should see the app running with a text box at the top to search for items in the ListView.

## Conclusion
In this blog post, we learned how to create a searchable ListView in Flutter. By using the `TextField` widget and manipulating the list based on the search keywords, we were able to filter the items dynamically. This feature can be useful in various scenarios, such as searching for products in an e-commerce app or filtering through a list of contacts. Stay tuned for more Flutter tutorials!

#flutter #searchableListView