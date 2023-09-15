---
layout: post
title: "ListView with lazy loading: Implementing pagination in Flutter."
description: " "
date: 2023-09-15
tags: [flutter, pagination]
comments: true
share: true
---

In this tutorial, we will learn how to implement pagination using the `ListView` widget in Flutter. Pagination is a common pattern used in mobile and web applications to load data incrementally, improving the user experience and reducing the amount of data transfer.

## Getting Started

To get started, make sure you have Flutter installed on your machine. Then, create a new Flutter project and navigate to the project directory.

```bash
$ flutter create lazy_loading_example
$ cd lazy_loading_example
```

## Setting Up the Project

1. Open `pubspec.yaml` file and add the following dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter
  http: ^0.13.4
```

2. Run `flutter pub get` to install the required dependencies.

3. Replace the contents of `lib/main.dart` file with the following code:

```dart
import 'dart:convert';

import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Lazy Loading Example',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: HomePage(),
    );
  }
}

class HomePage extends StatefulWidget {
  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  List<int> _dataList = [];
  int _currentPage = 1;
  int _totalPages;
  bool _isLoading = false;

  @override
  void initState() {
    super.initState();
    _fetchData();
  }

  Future<void> _fetchData() async {
    if (_isLoading) return;

    try {
      setState(() {
        _isLoading = true;
      });

      final response = await http.get(Uri.parse(
          'https://api.example.com/data?page=$_currentPage&limit=10'));

      if (response.statusCode == 200) {
        final data = jsonDecode(response.body);
        final totalPages = data['total_pages'];
        final List<int> newDataList = List<int>.from(data['data']);

        setState(() {
          _totalPages = totalPages;
          _dataList.addAll(newDataList);
          _isLoading = false;
        });
      } else {
        throw Exception(
            'Failed to fetch data: ${response.statusCode} ${response.reasonPhrase}');
      }
    } catch (e) {
      setState(() {
        _isLoading = false;
      });
      print('Error: $e');
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Lazy Loading Example'),
      ),
      body: ListView.builder(
        itemCount: _dataList.length + 1,
        itemBuilder: (context, index) {
          if (index < _dataList.length) {
            return ListTile(
              title: Text('Item ${_dataList[index]}'),
            );
          } else if (_currentPage < _totalPages) {
            if (!_isLoading) {
              _currentPage++;
              _fetchData();
            }
            return Center(
              child: CircularProgressIndicator(),
            );
          } else {
            return SizedBox();
          }
        },
      ),
    );
  }
}
```

## Explanation

1. We start by creating a `ListView.builder` widget in the `body` of `HomePage`. This widget allows us to lazily load items as the user scrolls through the list.

2. In the `_HomePageState` class, we define the following:

- `_dataList`: A list to hold the fetched data.
- `_currentPage`: The current page number of the data to be fetched.
- `_totalPages`: The total number of pages available.
- `_isLoading`: A flag to indicate if data is currently being fetched.

3. In the `initState` method, we call `_fetchData` to fetch the initial set of data.

4. The `_fetchData` method sends an HTTP GET request to the API endpoint to fetch data. If the response is successful (status code 200), we parse the response body, update the `_dataList`, `_totalPages`, and `_isLoading` flags. If not, an exception is thrown.

5. In the `build` method, we check the index of the `ListView.builder` and return either a list item or a loading indicator based on the current state.

6. If the index is less than `_dataList.length`, we return a `ListTile` with the corresponding data item.

7. If the index is equal to `_dataList.length`, we check if there are more pages to fetch (`_currentPage < _totalPages`). If so, we increment the `_currentPage` and call `_fetchData` to trigger the fetch of the next page. We return a `CircularProgressIndicator` while the data is being fetched.

8. Finally, if there are no more pages to fetch, we return an empty `SizedBox`.

## Running the App

To run the app, use the following command:

```bash
$ flutter run
```

Now you have a `ListView` with lazy loading pagination in your Flutter application! Experiment with different API endpoints and customize the UI to fit your needs.

#flutter #pagination