---
layout: post
title: "Implementing lazy loading with offline support in Flutter"
description: " "
date: 2023-10-11
tags: []
comments: true
share: true
---

In this blog post, we will explore how to implement lazy loading with offline support in a Flutter application. Lazy loading is a technique used to load data progressively as the user scrolls, reducing the initial load time and improving performance. Offline support ensures that the application can fetch data from a local cache when there is no internet connection available.

## Table of Contents
- [Lazy Loading](#lazy-loading)
- [Offline Support](#offline-support)
- [Implementing Lazy Loading with Offline Support](#implementing-lazy-loading-with-offline-support)
    - [Step 1: Set up Dependencies](#step-1-set-up-dependencies)
    - [Step 2: Create a Data Provider](#step-2-create-a-data-provider)
    - [Step 3: Implement Lazy Loading](#step-3-implement-lazy-loading)
    - [Step 4: Integrate Offline Support](#step-4-integrate-offline-support)
- [Conclusion](#conclusion)

## Lazy Loading

Lazy loading can be implemented in Flutter using the `ListView.builder` widget, which creates items on-demand as the user scrolls. By setting the `itemCount` property dynamically based on the available data, the application fetches and renders only the necessary items, resulting in a more efficient data loading process.

## Offline Support

Offline support is crucial for applications that rely on network data. By storing fetched data in a local cache, the application can continue to display content even when there is no internet connectivity. The `flutter_cache_manager` package provides a simple way to manage caching in Flutter applications.

## Implementing Lazy Loading with Offline Support

### Step 1: Set up Dependencies

Start by adding the necessary dependencies in your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  http: ^0.13.0
  flutter_cache_manager: ^3.0.2
```

Then, install the dependencies by running `flutter pub get` command in your terminal.

### Step 2: Create a Data Provider

Create a data provider class that handles fetching data from the API and caching it locally. This provider will be responsible for managing the lazy loading and offline support logic.

```dart
import 'package:http/http.dart' as http;
import 'package:flutter_cache_manager/flutter_cache_manager.dart';

class DataProvider {
  final String apiUrl = 'https://api.example.com/data';
  final BaseCacheManager cacheManager = DefaultCacheManager();

  Future<List<String>> fetchData(int startIndex, int count) async {
    final response = await http.get(Uri.parse('$apiUrl?start=$startIndex&count=$count'));

    if (response.statusCode == 200) {
      return List<String>.from(jsonDecode(response.body));
    } else {
      throw Exception('Failed to fetch data');
    }
  }

  Future<FileInfo?> getCachedData() async {
    return cacheManager.getFileFromCache(apiUrl);
  }
}
```

### Step 3: Implement Lazy Loading

In your Flutter widget, use the `ListView.builder` widget to create a lazy loading list. Update the `itemCount` property based on the available data to fetch and render new items as the user scrolls.

```dart
import 'package:flutter/material.dart';

class LazyLoadingList extends StatefulWidget {
  @override
  _LazyLoadingListState createState() => _LazyLoadingListState();
}

class _LazyLoadingListState extends State<LazyLoadingList> {
  final DataProvider dataProvider = DataProvider();
  final int itemsPerPage = 20;
  int startIndex = 0;
  List<String> items = [];

  @override
  void initState() {
    super.initState();
    fetchData();
  }

  Future<void> fetchData() async {
    final data = await dataProvider.fetchData(startIndex, itemsPerPage);
    setState(() {
      items.addAll(data);
      startIndex += itemsPerPage;
    });
  }

  @override
  Widget build(BuildContext context) {
    return ListView.builder(
      itemCount: items.length + 1,
      itemBuilder: (BuildContext context, int index) {
        if (index == items.length) {
          fetchData();
          return CircularProgressIndicator();
        }
        return ListTile(
          title: Text(items[index]),
        );
      },
    );
  }
}
```

### Step 4: Integrate Offline Support

To add offline support, use the `flutter_cache_manager` package to fetch the data from the local cache if available. If the data is not cached or an error occurs, fallback to fetching data from the API.

```dart
Future<void> fetchData() async {
  final cachedData = await dataProvider.getCachedData();

  if (cachedData != null) {
    final cachedItems = List<String>.from(jsonDecode(cachedData.file.path));
    setState(() {
      items.addAll(cachedItems);
      startIndex += itemsPerPage;
    });
  } else {
    final data = await dataProvider.fetchData(startIndex, itemsPerPage);
    setState(() {
      items.addAll(data);
      startIndex += itemsPerPage;
    });
  }
}
```

## Conclusion

In this blog post, we have learned how to implement lazy loading with offline support in a Flutter application. By using the ListView.builder widget and managing a local cache of fetched data, we can provide a more efficient user experience and ensure that content is still available even without an internet connection.

#flutter #flutterdevelopment