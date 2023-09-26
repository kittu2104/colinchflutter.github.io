---
layout: post
title: "How to handle request headers in Flutter using the http package?"
description: " "
date: 2023-09-27
tags: []
comments: true
share: true
---

When making API requests in Flutter using the http package, you may need to include custom headers in the request. Request headers can be used for authentication, specifying content types, caching, and more. In this tutorial, we will explore how to handle request headers in Flutter using the http package.

## Step 1: Import the http package

First, you need to import the http package in your Flutter project. Open your project's `pubspec.yaml` file and add the http package in the dependencies section:

```yaml
dependencies:
  http: ^0.13.3
```

Save the file and run `flutter pub get` on your terminal to fetch the package.

## Step 2: Make a request with custom headers

To include custom headers in your API request, you can make use of the `headers` parameter provided by the http package. Here's an example of making a GET request with custom headers:

```dart
import 'package:http/http.dart' as http;

void fetchUsers() async {
  final url = Uri.parse('https://api.example.com/users');
  final headers = {
    'Authorization': 'Bearer your_token_here',
    'Content-Type': 'application/json',
  };

  final response = await http.get(url, headers: headers);

  if (response.statusCode == 200) {
    // Request was successful, handle the response
    print(response.body);
  } else {
    // Request failed, handle the error
    print('Request failed with status: ${response.statusCode}');
  }
}
```

In this example, we define the `url` and `headers` variables. The `headers` map contains key-value pairs of the headers you want to include in the request. In this case, we include an `Authorization` header with a bearer token and a `Content-Type` header with the value `application/json`.

We then make the GET request using `http.get()` and pass the `headers` map as the value for the `headers` parameter.

## Step 3: Handling the response

In the example code above, we handle the response based on the status code returned by the API. If the status code is 200, the request was successful, and we can handle the response data. Otherwise, if the status code is different, we handle the error.

Remember to replace `'https://api.example.com/users'` with the actual API endpoint you want to request.

## Conclusion

Handling request headers in Flutter using the http package is straightforward. By including custom headers in your API requests, you can authenticate, specify content types, and perform other actions required by the API you're interacting with.