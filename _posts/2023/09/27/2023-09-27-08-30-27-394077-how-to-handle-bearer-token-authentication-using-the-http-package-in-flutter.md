---
layout: post
title: "How to handle Bearer token authentication using the http package in Flutter?"
description: " "
date: 2023-09-27
tags: []
comments: true
share: true
---

In this blog post, we will explore how to handle Bearer token authentication in Flutter using the `http` package. Bearer token authentication, commonly used in RESTful APIs, involves including a token in the `Authorization` header of every request to authenticate the user.

## Prerequisites
Before we proceed, make sure you have Flutter installed on your machine. You can follow the official documentation to get started: [Flutter Installation Guide](https://flutter.dev/docs/get-started/install)

## Getting Started
Let's begin by adding the `http` package as a dependency in our `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  http: ^0.13.3
```

After adding the dependency, run `flutter pub get` to fetch and install the package.

## Implementing Bearer Token Authentication
To authenticate API requests with a Bearer token, we need to add the token to the `Authorization` header of each request.

Here's an example of how to perform API requests with Bearer token authentication:

First, import the necessary packages:

```dart
import 'dart:convert';
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;
```

Next, define a function that performs the API request:

```dart
Future<Map<String, dynamic>> fetchData() async {
  final url = Uri.parse('https://api.example.com/data');
  final token = 'your_bearer_token';

  final response = await http.get(
    url,
    headers: {'Authorization': 'Bearer $token'},
  );

  if (response.statusCode == 200) {
    return json.decode(response.body);
  } else {
    throw Exception('Failed to load data');
  }
}
```
Replace `'https://api.example.com/data'` with the actual endpoint URL, and `'your_bearer_token'` with the token value provided by the server.

Finally, call the `fetchData` function whenever you need to make authenticated API requests:

```dart
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Bearer Token Authentication',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Bearer Token Authentication'),
        ),
        body: Center(
          child: ElevatedButton(
            child: Text('Fetch Data'),
            onPressed: () {
              fetchData().then((data) {
                // Handle API response data
              }).catchError((error) {
                // Handle error
              });
            },
          ),
        ),
      ),
    );
  }
}
```

In the above code, we have a simple Flutter app with a button that triggers the API request when pressed. You can replace the `onPressed` callback with your own logic to handle the API response or errors.

That's it! You have now implemented Bearer token authentication using the `http` package in Flutter.

## Conclusion
In this blog post, we learned how to handle Bearer token authentication in Flutter using the `http` package. By including the token in the `Authorization` header of each request, we can securely authenticate with API endpoints. Feel free to explore further customization and error handling based on your specific needs.

#flutter #fluttertutorial