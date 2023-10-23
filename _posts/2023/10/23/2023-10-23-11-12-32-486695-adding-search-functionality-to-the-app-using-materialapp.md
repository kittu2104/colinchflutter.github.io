---
layout: post
title: "Adding search functionality to the app using MaterialApp."
description: " "
date: 2023-10-23
tags: [MaterialApp]
comments: true
share: true
---

In this tech blog post, we will explore how to add search functionality to your app using the `MaterialApp` widget in Flutter. The `MaterialApp` provides a variety of widgets and features for building beautiful and functional UIs.

## Table of Contents
- [Introduction](#introduction)
- [Implementation](#implementation)
- [Example Code](#example-code)
- [Conclusion](#conclusion)
- [References](#references)
- [Tags](#tags)

## Introduction

Implementing search functionality in your app can greatly enhance user experience and improve the app's usability. With the help of the `MaterialApp` widget in Flutter, you can easily integrate a search feature into your app.

## Implementation

To implement search functionality using `MaterialApp`, you need to follow these steps:

1. Define a search field widget to capture user input.
2. Create a list of items to search within.
3. Implement the search logic to filter the list based on user input.
4. Display the search results.

Let's dive into each step in more detail.

1. **Define a search field widget**: Use the `TextField` widget from the `material` package to create an input field for users to enter their search query.

```dart
TextField(
  onChanged: (value) {
    // Implement search logic here
  },
  decoration: InputDecoration(
    labelText: 'Search',
    prefixIcon: Icon(Icons.search),
  ),
)
```

2. **Create a list of items**: Define a list of items that you want to search within. This could be a list of strings or a list of custom objects, depending on your app's requirements.

```dart
List<String> itemList = [
  'Apple',
  'Banana',
  'Orange',
  'Mango',
  'Pineapple',
];
```

3. **Implement the search logic**: Inside the `onChanged` callback of the `TextField`, implement the search logic to filter the list of items based on the user's input.

```dart
List<String> searchResults = [];

void searchItems(String query) {
  searchResults = itemList.where((item) =>
      item.toLowerCase().contains(query.toLowerCase())).toList();
}
```

4. **Display the search results**: Finally, display the search results in the UI using a ListView or any other widget of your choice.

```dart
ListView.builder(
  itemCount: searchResults.length,
  itemBuilder: (BuildContext context, int index) {
    return ListTile(
      title: Text(searchResults[index]),
    );
  },
)
```

## Example Code

Here's an example of how you can integrate search functionality using `MaterialApp` in Flutter:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(SearchApp());
}

class SearchApp extends StatelessWidget {
  final List<String> itemList = [
    'Apple',
    'Banana',
    'Orange',
    'Mango',
    'Pineapple',
  ];

  List<String> searchResults = [];

  void searchItems(String query) {
    searchResults = itemList.where((item) =>
        item.toLowerCase().contains(query.toLowerCase())).toList();
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Search App',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Search App'),
        ),
        body: Column(
          children: [
            TextField(
              onChanged: searchItems,
              decoration: InputDecoration(
                labelText: 'Search',
                prefixIcon: Icon(Icons.search),
              ),
            ),
            Expanded(
              child: ListView.builder(
                itemCount: searchResults.length,
                itemBuilder: (BuildContext context, int index) {
                  return ListTile(
                    title: Text(searchResults[index]),
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

## Conclusion

By using the `MaterialApp` widget in Flutter, you can easily add search functionality to your app, enabling users to search for specific items or content within your app. This not only enhances the user experience but also improves the overall usability of your app.

Try implementing this feature in your next Flutter app and see how it enhances the user experience!

## References
- [Flutter Documentation](https://flutter.dev/docs)
- [Flutter Material package Documentation](https://pub.dev/packages/material)

## Tags
#Flutter #MaterialApp