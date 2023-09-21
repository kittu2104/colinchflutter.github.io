---
layout: post
title: "Handling data fetching and API calls in Flutter SSR"
description: " "
date: 2023-09-21
tags: [FlutterSSR, APICalls]
comments: true
share: true
---

Flutter is a popular cross-platform framework that allows developers to build high-performance native apps for various platforms, including mobile, web, and desktop. With the introduction of server-side rendering (SSR) support in Flutter, developers can now render Flutter apps on the server and send pre-rendered HTML to the client.

When building an SSR app, handling data fetching and API calls is a critical aspect. In this blog post, we will explore different approaches to handle data fetching and API calls in Flutter SSR.

## 1. Using package:http

Flutter provides the **package:http** library, which allows you to make HTTP requests to fetch data from APIs. Since the server-side environment lacks the UI rendering capabilities of the client-side, you need to utilize the server-side version of the HTTP package. You can add the following dependency to your pubspec.yaml file:

```
dependencies:
  http: ^0.13.4
```

Here's an example of how you can make an API call using the **http** package in Flutter SSR:

```dart
import 'package:http/http.dart' as http;

Future<String> fetchData() async {
  final response = await http.get(Uri.parse('https://api.example.com/data'));
  if (response.statusCode == 200) {
    return response.body;
  } else {
    throw Exception('Failed to fetch data');
  }
}

void main() async {
  final data = await fetchData();
  // Use the fetched data to render the UI
}
```

Make sure to use the server-side version of the **http** package by importing it as **http**. If the API response is successful, you can use the fetched data to render the UI on the server.

## 2. Using package:dio

Another popular package for making API calls in Flutter is **package:dio**. It provides a more powerful and flexible way to handle HTTP requests. You can add the following dependency to your pubspec.yaml file:

```
dependencies:
  dio: ^4.0.0
```

Here's an example of how you can make an API call using the **dio** package in Flutter SSR:

```dart
import 'package:dio/dio.dart';

Future<String> fetchData() async {
  final dio = Dio();
  final response = await dio.get('https://api.example.com/data');
  if (response.statusCode == 200) {
    return response.data;
  } else {
    throw Exception('Failed to fetch data');
  }
}

void main() async {
  final data = await fetchData();
  // Use the fetched data to render the UI
}
```

The **dio** package offers advanced features like interceptors, request cancellation, and form data handling, making it a convenient choice for handling API calls in Flutter SSR.

## Conclusion

In this blog post, we explored two popular approaches to handle data fetching and API calls in Flutter SSR. Whether you choose to use the **http** package or the **dio** package, it's crucial to make API calls on the server and utilize the pre-rendered data to render the UI.

By efficiently handling data fetching and API calls in Flutter SSR, you can create dynamic and interactive server-rendered apps that deliver a smooth user experience. #FlutterSSR #APICalls