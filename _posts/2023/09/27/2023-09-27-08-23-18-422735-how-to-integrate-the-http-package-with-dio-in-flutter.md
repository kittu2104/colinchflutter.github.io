---
layout: post
title: "How to integrate the http package with Dio in Flutter?"
description: " "
date: 2023-09-27
tags: []
comments: true
share: true
---

When working with network requests in Flutter, you have multiple options for making HTTP requests. Two popular packages for handling network requests are the `http` package and the `Dio` package. In this tutorial, we will learn how to integrate the `http` package with `Dio` to take advantage of the features provided by both packages.

## Step 1: Adding dependencies

First, you need to add the necessary dependencies to your `pubspec.yaml` file. Open the `pubspec.yaml` file and add the following lines:

```yaml
dependencies:
  flutter:
    sdk: flutter
  http: ^0.13.0
  dio: ^4.0.0
```

Save the file and run `flutter pub get` in your terminal to fetch and install the dependencies.

## Step 2: Importing the packages

In your Dart file, import both `http` and `dio` packages using the following statements:

```dart
import 'package:http/http.dart' as http;
import 'package:dio/dio.dart';
```

## Step 3: Making HTTP requests with `http`

To make an HTTP request using the `http` package, you can use the `get()` method, which returns a `Future<http.Response>`. Here's an example of making a GET request:

```dart
void makeHttpRequest() async {
  final response = await http.get(Uri.parse('https://api.example.com/data'));
  
  if (response.statusCode == 200) {
    print(response.body);
  } else {
    print('Request failed with status: ${response.statusCode}');
  }
}
```

## Step 4: Making HTTP requests with `Dio`

Similarly, to make an HTTP request using the `Dio` package, you need to create a new instance of the `Dio` class and use its methods. Here's an example of making a GET request:

```dart
void makeDioRequest() async {
  final dio = Dio();
  
  try {
    final response = await dio.get('https://api.example.com/data');
    print(response.data);
  } catch (e) {
    print('Request failed with error: $e');
  }
}
```

## Step 5: Combining `http` with `Dio`

To combine the functionalities of `http` and `Dio`, you can use the `DioAdapter` class provided by the `Dio` package. The `DioAdapterHttp2Handler` class implements the `HttpClientAdapter` interface required by `http`. Here's an example of integrating `http` with `Dio`:

```dart
void integrateHttpWithDio() async {
  final dio = Dio();
  final adapter = DioAdapter();

  dio.httpClientAdapter = adapter;

  final response = await dio.get('https://api.example.com/data');
  
  if (response.statusCode == 200) {
    print(response.data);
  } else {
    print('Request failed with status: ${response.statusCode}');
  }
}
```

In the above example, we create an instance of `Dio` and a `DioAdapter`. We then set the `httpClientAdapter` of `Dio` to the `DioAdapter` instance. This allows `Dio` to use the `http` package as its underlying HTTP client.

## Conclusion

By integrating the `http` package with `Dio`, you can leverage the features provided by both packages in your Flutter app. The `http` package provides a simple and convenient API for making HTTP requests, while `Dio` offers additional advanced features such as request cancellation and interceptors.