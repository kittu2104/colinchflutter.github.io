---
layout: post
title: "How to make PUT requests using the http package in Flutter?"
description: " "
date: 2023-09-27
tags: [HTTP]
comments: true
share: true
---

In Flutter, you can make PUT requests to update data on a server using the `http` package. The `http` package provides a convenient way to make HTTP requests and handle the responses in your Flutter applications.

## Prerequisites

Before you can make PUT requests, you need to add the `http` package to your dependencies in the `pubspec.yaml` file.

```yaml
dependencies:
  flutter:
    sdk: flutter
  http: ^0.13.3
```

Don't forget to run `flutter pub get` to fetch the package.

## Making the PUT Request

To make a PUT request in Flutter, follow these steps:

1. Import the necessary packages:

```dart
import 'dart:convert';
import 'package:http/http.dart' as http;
```

2. Define the URL and the payload data to be sent with the request:

```dart
final url = 'https://api.example.com/users/1';  // Replace with your API endpoint
final payload = {'name': 'John Doe', 'age': 30}; // Replace with your data
```

3. Make the PUT request using the `http.put` method, and handle the response:

```dart
try {
  final response = await http.put(
    Uri.parse(url),
    headers: <String, String>{
      'Content-Type': 'application/json',
    },
    body: jsonEncode(payload),
  );

  if (response.statusCode == 200) {
    print('PUT request successful');
  } else {
    print('PUT request failed with status: ${response.statusCode}');
  }
} catch (e) {
  print('Error: $e');
}
```

In the example above, we use the `jsonEncode` method from the `dart:convert` package to convert the payload data into a JSON string.

5. You can use the `response.statusCode` property to check the status of the request. If it is equal to 200, the request was successful. Otherwise, an error occurred.

Note: Don't forget to replace the `url` and `payload` variables with your own values according to your API.

## Conclusion

In this blog post, we learned how to make PUT requests in Flutter using the `http` package. We covered the necessary steps, including importing the package, defining the URL and payload data, making the request, and handling the response. This knowledge will help you update data on a server in your Flutter applications. #Flutter #HTTP