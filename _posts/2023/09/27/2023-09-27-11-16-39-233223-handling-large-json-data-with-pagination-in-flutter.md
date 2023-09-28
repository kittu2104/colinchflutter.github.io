---
layout: post
title: "Handling large JSON data with pagination in Flutter"
description: " "
date: 2023-09-27
tags: [Flutter, pagination]
comments: true
share: true
---

Handling large JSON data in Flutter can be challenging, especially when it exceeds the device's memory limit. One way to tackle this issue is by implementing pagination, which allows you to load data in smaller chunks gradually. In this blog post, we will explore how to handle large JSON data with pagination in Flutter.

## Step 1: Fetching initial data

To begin, you need to fetch the initial data for your widget. The data can be retrieved from an API endpoint or a local JSON file. Here's an example of using the `http` package in Flutter to make an API request and retrieve the initial data:

```dart
import 'dart:convert';
import 'package:http/http.dart' as http;

Future<List<dynamic>> fetchInitialData() async {
  final response = await http.get('https://api.example.com/endpoint');
  final parsed = json.decode(response.body);
  return parsed['data'];
}
```

## Step 2: Implementing pagination

To implement pagination, you need to keep track of the current page and the number of items per page. You can use a state management solution like `Provider` or `Bloc` to manage the state of your widget.

```dart
int currentPage = 1;
int itemsPerPage = 10;
List<dynamic> data = [];

Future<void> fetchNextDataPage() async {
  final response = await http.get('https://api.example.com/endpoint?page=$currentPage&limit=$itemsPerPage');
  final parsed = json.decode(response.body);
  final newData = parsed['data'];
  data.addAll(newData);
  currentPage++;
}
```

In the code above, `fetchNextDataPage()` is called whenever you want to load the next page of data. It appends the new data to the existing `data` list and increments the `currentPage` variable.

## Step 3: Displaying the paginated data

Now that you have implemented pagination, you can display the paginated data in your widget. You can use a `ListView.builder` to dynamically load and display the data as the user scrolls.

```dart
ListView.builder(
  itemCount: data.length + 1, // +1 for loading indicator
  itemBuilder: (BuildContext context, int index) {
    if (index == data.length) {
      // Reached the end, show loading indicator
      return CircularProgressIndicator();
    }
    return ListTile(
      title: Text(data[index]['title']),
      subtitle: Text(data[index]['description']),
    );
  },
  onEndReached: () async {
    // Load next page when reaching the end
    await fetchNextDataPage();
    setState(() {});
  },
);
```

In this code snippet, the `ListView.builder` renders the paginated data as list tiles. The `itemCount` is set to `data.length + 1` to account for the loading indicator at the end. The `onEndReached` callback is triggered when the user reaches the end of the current list, and it calls `fetchNextDataPage()` to load the next page of data.

## Conclusion

With pagination, you can efficiently handle large JSON data in Flutter without overwhelming the device's memory. By fetching data in smaller chunks and dynamically loading it as the user scrolls, you can provide a smooth and efficient user experience. Use the code snippets provided in this blog post as a starting point and adapt them to your specific use case to handle large JSON data with pagination in your Flutter app.

#Flutter #pagination