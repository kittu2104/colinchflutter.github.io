---
layout: post
title: "How to handle redirections in http requests using the http package in Flutter?"
description: " "
date: 2023-09-27
tags: [http, redirections]
comments: true
share: true
---

Handling redirections in HTTP requests is essential when working with APIs or when dealing with web resources that have changed location. In Flutter, the `http` package provides easy-to-use methods for making HTTP requests and handling different response statuses, including redirections.

In this tutorial, we will learn how to handle redirections using the `http` package in Flutter.

## Step 1: Install the `http` Package

To begin, make sure you have the `http` package added to your `pubspec.yaml` file. Open your project's `pubspec.yaml` file and add the following line under `dependencies`:

```yaml
dependencies:
  http: ^0.13.3
```

Save the file and run `flutter pub get` to install the package.

## Step 2: Making an HTTP Request

To handle redirections, we will use the `get` method from the `http` package. This method allows us to make an HTTP GET request to a specified URL.

```dart
import 'package:http/http.dart' as http;

void main() async {
  final response = await http.get(Uri.parse('https://example.com'));

  print(response.statusCode);
  print(response.body);
}
```

In the above code, we import the `http` package and use the `get` method to make an HTTP GET request to `https://example.com`. The `get` method returns a `Future<Response>`, so we `await` the response and store it in the `response` variable.

## Step 3: Handling Redirections

By default, the `http` package automatically follows redirections. This means that if the server responds with a redirect status code (3xx), the `http` package will automatically send another request to the new location.

To check if a redirection occurred, we can use the `isRedirect` property of the `Response` object:

```dart
if (response.isRedirect) {
  final redirectedUrl = response.headers['location'];
  print('Redirected URL: $redirectedUrl');
}
```

In the above code, we check if the `isRedirect` property of the `response` is `true`. If it is, we can access the new location URL using the `location` header.

This allows us to handle redirections and take any necessary actions based on the new location.

## Conclusion

Handling redirections is an important aspect of working with HTTP requests in Flutter. The `http` package provides a simple and convenient way to handle redirections by default.

In this tutorial, we learned how to install the `http` package, make an HTTP request, and handle redirections using the `http` package in Flutter.

#flutter #http #redirections