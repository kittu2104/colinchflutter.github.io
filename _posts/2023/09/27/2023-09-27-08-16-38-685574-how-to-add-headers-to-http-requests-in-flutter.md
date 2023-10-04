---
layout: post
title: "How to add headers to http requests in Flutter?"
description: " "
date: 2023-09-27
tags: [HTTPRequests]
comments: true
share: true
---

When making HTTP requests in Flutter, you might need to include headers to provide additional information or authentication credentials to the server. In this blog post, we will discuss how to add headers to your HTTP requests in Flutter.

## Step 1: Import the necessary packages

To include headers in your HTTP requests, you need to import the `http` package. Open your Flutter project's `pubspec.yaml` file and add the following dependency:

```yaml
dependencies:
  http: ^0.13.0
```

Save the file and run `flutter pub get` to install the package.

## Step 2: Add headers to the HTTP request

To add headers to a specific HTTP request, you need to create a `Map<String, String>` object and pass it as the `headers` parameter in the HTTP request.

Here's an example of adding a custom header to a GET request:

```dart
import 'package:http/http.dart' as http;

void getRequestWithHeaders() async {
  String url = 'https://api.example.com/data';
  
  Map<String, String> headers = {
    'Authorization': 'Bearer YOUR_AUTH_TOKEN',
    'Content-Type': 'application/json',
  };
  
  http.Response response = await http.get(Uri.parse(url), headers: headers);
  
  if (response.statusCode == 200) {
    // Handle successful response
  } else {
    // Handle error response
  }
}
```

In this example, we include two headers: `Authorization` for providing an authentication token and `Content-Type` for specifying the request's content type.

## Step 3: Send the HTTP request with headers

To send the HTTP request with the added headers, you can use the appropriate method from the `http` package (e.g., `http.get`, `http.post`, etc.).

In the above example, we used `http.get` to send a GET request. You can replace it with other HTTP methods based on your requirements.

## Conclusion

Adding headers to your HTTP requests in Flutter is essential for providing additional information or authentication credentials to the server. By following the steps mentioned in this blog post, you can easily include headers in your Flutter app's HTTP requests.

#Flutter #HTTPRequests #Headers