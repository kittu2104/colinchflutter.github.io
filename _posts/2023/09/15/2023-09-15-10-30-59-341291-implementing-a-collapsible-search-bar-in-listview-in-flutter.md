---
layout: post
title: "Implementing a collapsible search bar in ListView in Flutter."
description: " "
date: 2023-09-15
tags: [Flutter, ListView, SearchBar]
comments: true
share: true
---

In this blog post, we will explore how to implement a collapsible search bar in a ListView in Flutter. This feature can improve the user experience by allowing them to easily search and filter the items in the ListView.

## Prerequisites

Before diving into the implementation, make sure you have the following:

- Flutter SDK installed on your machine
- Flutter project set up

## Steps to Implement

### Step 1: Add Flutter packages

Firstly, open your **pubspec.yaml** file and add the `flutter_search_bar` package as a dependency:

```yaml
dependencies:
  flutter_search_bar: ^1.1.3
```

Save the file and run `flutter pub get` in the terminal to fetch the package.

### Step 2: Create the ListView

In your Flutter project, create a ListView and populate it with the desired items. You can use a `ListView.builder` widget to efficiently build the list from a data source.

```dart
ListView.builder(
  itemCount: _items.length,
  itemBuilder: (context, index) {
    return ListTile(
      title: Text(_items[index]),
    );
  },
)
```

### Step 3: Implement the collapsible search bar

Now, we need to wrap the ListView with a widget that provides a collapsible search bar functionality. We will use the `SearchBar` widget from the `flutter_search_bar` package.

```dart
import 'package:flutter_search_bar/flutter_search_bar.dart';

SearchBar searchBar = SearchBar(
  hintText: 'Search...',
  setState: setState,
  onSubmitted: (value) {
    // Implement the search logic here
    // Update the ListView based on the search results
  },
);

@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: searchBar.build(context),
    body: searchBar.isSearching ? _buildSearchListView() : _buildDefaultListView(),
  );
}

Widget _buildDefaultListView() {
  return ListView.builder(
    itemCount: _items.length,
    itemBuilder: (context, index) {
      return ListTile(
        title: Text(_items[index]),
      );
    },
  );
}

Widget _buildSearchListView() {
  // Implement the logic to filter the ListView based on search input
  // Return the filtered ListView
}

@override
void initState() {
  super.initState();
  searchBar = SearchBar(
    hintText: 'Search...',
    setState: setState,
    onSubmitted: (value) {
      // Implement the search logic here
      // Update the ListView based on the search results
    },
  );
}

@override
void dispose() {
  searchBar.dispose();
  super.dispose();
}
```

### Step 4: Adjust ListView based on search input

To update the ListView based on the search input, implement the filtering logic in the `_buildSearchListView()` method. This method should return a ListView with the filtered items.

```dart
Widget _buildSearchListView() {
  final List<String> filteredItems = _items.where(
    (item) => item.toLowerCase().contains(searchBar.getSearchTerm().toLowerCase()),
  ).toList();

  return ListView.builder(
    itemCount: filteredItems.length,
    itemBuilder: (context, index) {
      return ListTile(
        title: Text(filteredItems[index]),
      );
    },
  );
}
```

## Conclusion

By following the steps outlined in this blog post, you can implement a collapsible search bar in a ListView in your Flutter app. This feature allows users to search and filter the items, improving the overall user experience.

Let us know in the comments below if you found this tutorial helpful or if you have any questions!

#Flutter #ListView #SearchBar