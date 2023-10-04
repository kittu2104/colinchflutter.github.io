---
layout: post
title: "How to add query parameters to http requests in Flutter?"
description: " "
date: 2023-09-27
tags: [HTTPRequest]
comments: true
share: true
---

When making HTTP requests in a Flutter app, you may often need to attach query parameters to the URL. Query parameters are key-value pairs that are appended to the URL, allowing you to pass additional information to the server.

In Flutter, you can easily add query parameters to HTTP requests using the `Uri` class from the `dart:core` library. Here's how you can do it:

```dart
import 'dart:convert';
import 'package:http/http.dart' as http;

void sendRequestWithQueryParameters() async {
  final Uri uri = Uri.parse('https://api.example.com/api/posts');
  final Map<String, String> queryParams = {
    'category': 'technology',
    'sort': 'latest',
  };

  final url = uri.replace(queryParameters: queryParams);
  
  final response = await http.get(url);
  
  if (response.statusCode == 200) {
    final responseBody = json.decode(response.body);
    // Handle the response data
  } else {
    print('Request failed with status: ${response.statusCode}');
  }
}
```

In the above code snippet, we create a `Uri` object from the base URL. Then, we define a `Map` of query parameters where the keys represent the parameter names and the values represent their corresponding values.

We use the `replace` method of the `Uri` object to replace the query parameters with the ones we defined. The resulting `Uri` object will have the query parameters appended to the URL.

Finally, we make an HTTP GET request using the modified URL and handle the response accordingly. Note that we use the `http` package to send the HTTP request and decode the response using the `json` package.

Remember to include the necessary dependencies in your `pubspec.yaml` file:

```yaml
dependencies:
  http: ^0.13.3
```

By adding query parameters to your HTTP requests in Flutter, you can pass additional data to the server and retrieve the desired results. This is particularly useful when working with APIs that require specific parameters to be included in the URL. #Flutter #HTTPRequest