---
layout: post
title: "Implementing lazy loading with pagination in Flutter"
description: " "
date: 2023-10-11
tags: [lazyloading]
comments: true
share: true
---

In modern mobile app development, it's crucial to provide a smooth and efficient user experience. One way to achieve this is by implementing lazy loading with pagination, especially when dealing with large amounts of data in your Flutter app. Lazy loading allows you to load data in chunks as needed, instead of loading everything at once, which can significantly improve app performance and reduce resource consumption.

In this blog post, we will explore how to implement lazy loading with pagination in Flutter using the `ListView.builder` widget and an example API to fetch data.

## Table of Contents
- [Setting up the project](#setting-up-the-project)
- [Implementing lazy loading](#implementing-lazy-loading)
- [Using pagination](#using-pagination)
- [Conclusion](#conclusion)

## Setting up the project

Before we dive into the implementation, make sure you have a Flutter project set up. If you haven't, you can create a new Flutter project using the following command:

```dart
flutter create lazy_loading_pagination
```

Next, open the project in your favorite IDE and navigate to the `lib` directory. Inside, create a new file called `lazy_loading_pagination.dart`, which will contain our implementation.

## Implementing lazy loading

To implement lazy loading, we'll use the `ListView.builder` widget provided by Flutter. The `ListView.builder` widget is designed to efficiently display a large list of items by creating a widget for each item that is visible on the screen.

First, import the necessary Flutter packages at the top of the `lazy_loading_pagination.dart` file:

```dart
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;
import 'dart:convert';
```

Next, let's define a stateful widget called `LazyLoadingPagination`:

```dart
class LazyLoadingPagination extends StatefulWidget {
  @override
  _LazyLoadingPaginationState createState() => _LazyLoadingPaginationState();
}
```

Inside the state class `_LazyLoadingPaginationState`, we'll define some variables to keep track of the loaded data and the current page:

```dart
class _LazyLoadingPaginationState extends State<LazyLoadingPagination> {
  List<String> data = [];
  int currentPage = 1;
  bool isLoading = false;
  ScrollController _scrollController = ScrollController();

  @override
  void initState() {
    super.initState();
    fetchData();
    _scrollController.addListener(_scrollListener);
  }
  
  @override
  void dispose() {
    _scrollController.dispose();
    super.dispose();
  }

  void _scrollListener() {
    if (_scrollController.offset >=
        _scrollController.position.maxScrollExtent &&
        !_scrollController.position.outOfRange) {
      fetchData();
    }
  }
  
  Future<void> fetchData() async {
    if (!isLoading) {
      setState(() {
        isLoading = true;
      });
      final response = await http.get("https://example.com/api/data?page=$currentPage");
      if (response.statusCode == 200) {
        List<String> newData = json.decode(response.body);
        setState(() {
          data.addAll(newData);
          currentPage++;
          isLoading = false;
        });
      } else {
        throw Exception('Failed to load data');
      }
    }
  }
  
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Lazy Loading Pagination'),
      ),
      body: ListView.builder(
        controller: _scrollController,
        itemCount: data.length + 1,
        itemBuilder: (BuildContext context, int index) {
          if (index == data.length) {
            return buildLoader();
          }
          return ListTile(
            title: Text(data[index]),
            // Rest of your list item UI
          );
        },
      ),
    );
  }
  
  Widget buildLoader() {
    return Padding(
      padding: const EdgeInsets.all(8.0),
      child: Center(
        child: CircularProgressIndicator(),
      ),
    );
  }
}
```

In the `fetchData` method, we make a HTTP GET request to an example API with a `page` query parameter that specifies the current page. If the response is successful, we parse the JSON response and update the `data` list. When building the ListView, we check for the index to determine whether to show the loader widget or the actual data item.

## Using pagination

The above implementation handles lazy loading by fetching new data when the user scrolls to the end of the list. However, you'll need to configure your API server to handle pagination and return a subset of data based on the page number.

Make sure to update the `fetchData` method with your actual API endpoint and adjust the parsing logic based on your API's response format.

## Conclusion

In this blog post, we learned how to implement lazy loading with pagination in Flutter using the `ListView.builder` widget. By fetching data in chunks as needed, we can greatly improve the performance of our Flutter app when dealing with large datasets. Remember to fine-tune the pagination logic for your specific use case and API.

For more information, you can check out the [ListView.builder documentation](https://api.flutter.dev/flutter/widgets/ListView/ListView.builder.html) or explore other pagination techniques in Flutter. Happy coding!

\#flutter #lazyloading