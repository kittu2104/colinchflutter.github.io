---
layout: post
title: "How to cancel http requests in Flutter using the http package?"
description: " "
date: 2023-09-27
tags: [http]
comments: true
share: true
---

In Flutter, the `http` package provides a convenient way to make HTTP requests. However, there may be situations where you need to cancel an ongoing HTTP request, especially in cases where the user navigates away from the current screen or performs some action that renders the request unnecessary.

Canceling HTTP requests is important to avoid wasting resources and to ensure the app's performance. Fortunately, the `http` package in Flutter provides an easy way to cancel requests using the `http.CancellationToken` class.

## Cancelling a Single Request

To cancel a single HTTP request, you need to create an instance of `http.CancellationTokenSource` and pass it to the request. Here's an example:

```dart
import 'package:http/http.dart' as http;

cancelHTTPRequest() async {
  final client = http.Client();
  final cancellationTokenSource = http.CancellationTokenSource();

  final url = 'https://api.example.com/data';
  final response = await http.get(url, cancelToken: cancellationTokenSource.token);

  // Handle the response here

  client.close();
}
```

In the above example, we create an instance of `http.CancellationTokenSource` and pass its token to the `cancelToken` parameter of `http.get`. If the request needs to be canceled, we can call `cancellationTokenSource.cancel()`.

## Cancelling Multiple Requests

If you need to cancel multiple HTTP requests at once, you can use the same `http.CancellationTokenSource` instance for all of them. Here's an example:

```dart
import 'package:http/http.dart' as http;

cancelMultipleHTTPRequests() async {
  final client = http.Client();
  final cancellationTokenSource = http.CancellationTokenSource();

  final urls = [
    'https://api.example.com/data1',
    'https://api.example.com/data2',
    'https://api.example.com/data3',
  ];

  final responses = await Future.wait(
    urls.map((url) => http.get(url, cancelToken: cancellationTokenSource.token)),
  );

  // Handle the responses here

  client.close();
}
```

In the above example, we create a single instance of `http.CancellationTokenSource` and pass its token to all the requests using the `cancelToken` parameter. To cancel all the requests, we can call `cancellationTokenSource.cancel()`.

## Summary

Canceling HTTP requests in Flutter using the `http` package is made simple with the `http.CancellationToken` class. By creating an instance of `http.CancellationTokenSource` and passing its token to the requests, you can easily cancel requests when necessary, improving the app's performance and resource utilization.

#flutter #http