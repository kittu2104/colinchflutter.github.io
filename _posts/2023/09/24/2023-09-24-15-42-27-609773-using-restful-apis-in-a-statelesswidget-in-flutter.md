---
layout: post
title: "Using RESTful APIs in a StatelessWidget in Flutter"
description: " "
date: 2023-09-24
tags: [flutter, APIs]
comments: true
share: true
---

Flutter provides a powerful framework for building cross-platform applications with a beautiful user interface. One common requirement in mobile app development is fetching data from a server using RESTful APIs. In this blog post, we will explore how to integrate RESTful APIs into a StatelessWidget in Flutter.

## Step 1: Add Dependencies

First, let's add the necessary dependencies to our `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  http: ^0.13.0
```

We will be using the `http` package to make HTTP requests.

## Step 2: Make HTTP Requests

Now, let's create a class that handles HTTP requests. Create a new file called `api_service.dart` and add the following code:

```dart
import 'dart:convert';
import 'package:http/http.dart' as http;

class ApiService {
  static const String baseUrl = 'https://api.example.com';

  Future<dynamic> fetchData() async {
    final response = await http.get(Uri.parse('$baseUrl/data'));
    if (response.statusCode == 200) {
      return jsonDecode(response.body);
    } else {
      throw Exception('Failed to fetch data');
    }
  }
}
```

In the code above, we define a `fetchData` method that sends an HTTP GET request to the API endpoint and returns the response as JSON. We also handle error scenarios by throwing an exception.

## Step 3: Create the StatelessWidget

Now, let's create our `ApiWidget` that extends `StatelessWidget` and calls the API service to fetch data. Replace the contents of your main file with the following code:

```dart
import 'package:flutter/material.dart';
import 'api_service.dart';

class ApiWidget extends StatelessWidget {
  final ApiService apiService = ApiService();

  @override
  Widget build(BuildContext context) {
    return FutureBuilder<dynamic>(
      future: apiService.fetchData(),
      builder: (BuildContext context, AsyncSnapshot<dynamic> snapshot) {
        if (snapshot.connectionState == ConnectionState.waiting) {
          return Center(child: CircularProgressIndicator());
        } else if (snapshot.hasError) {
          return Center(child: Text('Error: ${snapshot.error}'));
        } else {
          final data = snapshot.data;
          // Render UI using the fetched data
          return Text('Fetched data: $data');
        }
      },
    );
  }
}

void main() {
  runApp(ApiWidget());
}
```

In the code above, we create an instance of `ApiService`, and in the `build` method, we use `FutureBuilder` to handle the asynchronous API call. While waiting for the response, we show a loading indicator. If there is an error, we display an error message. If the data is successfully fetched, we render the UI using the fetched data.

## Conclusion

In this blog post, we learned how to integrate RESTful APIs into a `StatelessWidget` in Flutter. We covered the necessary steps to make HTTP requests using the `http` package and handle different states of the API response. This approach allows us to fetch data asynchronously and keep our UI responsive. With this knowledge, you can now easily integrate API calls into your Flutter applications and build powerful mobile experiences.

#flutter #APIs