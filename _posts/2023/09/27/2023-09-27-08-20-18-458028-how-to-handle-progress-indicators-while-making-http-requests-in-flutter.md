---
layout: post
title: "How to handle progress indicators while making http requests in Flutter?"
description: " "
date: 2023-09-27
tags: [progressindicator]
comments: true
share: true
---

In a Flutter application, it's common to make HTTP requests to interact with APIs and retrieve data. As the response time may vary, it's essential to provide a smooth user experience by indicating the progress of the request. One way to achieve this is by using progress indicators.

## Using a CircularProgressIndicator

Flutter provides a built-in widget called `CircularProgressIndicator` that can be utilized for displaying a circular progress indicator. To handle progress indicators while making HTTP requests, follow these steps:

1. Import the necessary packages:

```dart
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;
```

2. Create a `bool` variable to track the loading state and initiate it as `false`.

```dart
bool _isLoading = false;
```

3. Implement a method that makes the HTTP request and updates the loading state:

```dart
Future<void> fetchData() async {
  setState(() {
    _isLoading = true;
  });

  try {
    final response = await http.get(Uri.parse('https://api.example.com/data'));
    // Process the response data

    setState(() {
      _isLoading = false;
    });
  } catch (error) {
    // Handle error
    setState(() {
      _isLoading = false;
    });
  }
}
```

4. Use the `CircularProgressIndicator` within your widget tree conditionally based on the `_isLoading` variable:

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: Text('Your App'),
    ),
    body: _isLoading
        ? Center(
            child: CircularProgressIndicator(),
          )
        : YourDataWidget(),
    floatingActionButton: FloatingActionButton(
      onPressed: fetchData,
      child: Icon(Icons.refresh),
    ),
  );
}
```

In this example, if `_isLoading` is `true`, the `CircularProgressIndicator` is displayed, indicating that the request is in progress. Otherwise, the `YourDataWidget` is shown.

With this approach, you can provide a visual indicator to your users while handling HTTP requests in Flutter.

#flutter #progressindicator