---
layout: post
title: "How to handle local caching of http responses in Flutter using the http package."
description: " "
date: 2023-09-27
tags: [httpcaching]
comments: true
share: true
---

In mobile application development, optimizing network requests is crucial for providing a smooth user experience. One of the ways to optimize network requests is by implementing local caching of HTTP responses. This allows the app to store and retrieve previously fetched data from the device's local storage, reducing the need for frequent network calls.

In Flutter, we can achieve local caching of HTTP responses using the `http` package in combination with the `shared_preferences` package. The `http` package provides a flexible and powerful way to make HTTP requests, and the `shared_preferences` package allows us to store key-value pairs in the device's local storage.

## Setting up the Dependencies

To get started, we need to add the `http` and `shared_preferences` packages as dependencies in our `pubspec.yaml` file:

```yaml
dependencies:
  http: ^0.13.0
  shared_preferences: ^2.0.10
```

After adding the dependencies, run `flutter pub get` to fetch and update the packages.

## Implementing Local Caching

First, let's import the necessary packages:

```dart
import 'package:http/http.dart' as http;
import 'package:shared_preferences/shared_preferences.dart';
```

Next, we'll create a helper function to handle HTTP requests with caching:

```dart
Future<http.Response> getWithCache(String url) async {
  final prefs = await SharedPreferences.getInstance();
  final cacheKey = 'http_cache:$url';

  // Check if the response is already stored in the cache
  if (prefs.containsKey(cacheKey)) {
    final cachedResponse = prefs.getString(cacheKey);
    if (cachedResponse != null) {
      return http.Response(cachedResponse, 200);
    }
  }

  // Make the HTTP request and store the response in the cache
  final response = await http.get(Uri.parse(url));
  if (response.statusCode == 200) {
    prefs.setString(cacheKey, response.body);
  }

  return response;
}
```

In this function:
- We first retrieve an instance of `SharedPreferences` using `SharedPreferences.getInstance()`.
- We generate a unique `cacheKey` for each URL.
- We check if the response is already stored in the cache by querying the `SharedPreferences` using the `cacheKey`.
- If the response is found in the cache, we create a new `http.Response` object with the cached response and return it.
- If the response is not found in the cache, we make the HTTP request using `http.get()`. If the response is successful (with status code 200), we store the response body in the cache using the `SharedPreferences` API.

Now, you can use the `getWithCache()` function to make HTTP requests with caching:

```dart
final response = await getWithCache('https://api.example.com/data');
if (response.statusCode == 200) {
  // Process the response data
} else {
  // Handle error
}
```

## Conclusion

Implementing local caching of HTTP responses in your Flutter app using the `http` package can significantly improve the performance and reduce the reliance on network calls. By combining the power of the `http` package and the `shared_preferences` package, you can easily enable local caching in your app and provide a seamless user experience.

#flutter #httpcaching