---
layout: post
title: "How to set request timeouts in the http package in Flutter?"
description: " "
date: 2023-09-27
tags: [Flutter, HTTP]
comments: true
share: true
---

When making HTTP requests in Flutter using the `http` package, it is important to handle request timeouts. A request timeout occurs when the server takes too long to respond to a request. To prevent the request from hanging indefinitely, you can set a timeout value.

By default, the `http` package does not have a built-in timeout mechanism. However, you can set a timeout value using the `http` package along with the `Dio` package which provides more extensive functionality, including request timeouts.

## Adding `Dio` to Your Flutter Application

To use the `Dio` package in your Flutter application, you need to add it as a dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  dio: ^3.0.10
```

After adding the dependency, run `flutter pub get` to fetch and update the package.

## Setting the Request Timeout

To set the request timeout using the `Dio` package, you can use the `Options` class and pass it to the `options` parameter when making the request.

Here's an example that sets a timeout of 5 seconds for an HTTP GET request:

```dart
import 'package:dio/dio.dart';

void fetchData() async {
  Dio dio = Dio();
  dio.options.connectTimeout = 5000; // 5 seconds
  dio.options.receiveTimeout = 5000; // 5 seconds

  try {
    Response response = await dio.get('https://api.example.com/data');
    print(response.data);
  } catch (e) {
    print('Request failed or timed out: $e');
  }
}
```

In the above code, we create a new instance of the `Dio` class and set the `connectTimeout` and `receiveTimeout` properties of the `options` object to 5000 milliseconds (5 seconds). If the request takes longer than the specified timeout, an exception will be thrown.

## Conclusion

Setting request timeouts is crucial when making HTTP requests in Flutter, as it helps prevent requests from hanging indefinitely. By using the `Dio` package, you can easily set the request timeouts and handle them gracefully in your Flutter application. Don't forget to handle potential exceptions that may occur due to the timeout to provide a better user experience.

#Flutter #HTTP #RequestTimeout