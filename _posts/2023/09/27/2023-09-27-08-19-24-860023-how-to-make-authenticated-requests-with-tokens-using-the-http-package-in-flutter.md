---
layout: post
title: "How to make authenticated requests with tokens using the http package in Flutter?"
description: " "
date: 2023-09-27
tags: [httppackage]
comments: true
share: true
---

In mobile app development, it's common to make authenticated API requests using tokens. In Flutter, we can accomplish this using the `http` package, which provides a simple way to make HTTP requests. In this blog post, we will explore how to make authenticated requests with tokens using the `http` package in Flutter.

### Step 1: Import `http` Package

First, we need to import the `http` package in our Flutter project. Open your project's `pubspec.yaml` file and add the `http` package to the dependencies section:

```
dependencies:
  Flutter:
    sdk: Flutter
  http: ^0.13.4
```

Save the file and run the command `flutter pub get` in your terminal to fetch the package.

### Step 2: Obtain Token

Before making authenticated requests, we need to obtain a token from the server. The process for obtaining a token may vary depending on the backend implementation. Once we have obtained the token, we can store it in Flutter's state management solution (e.g., Provider, Bloc) for easy access throughout the app.

### Step 3: Configure Authenticated Requests

To make authenticated requests, we need to include the token in the request headers. We can do this by setting the `Authorization` header to the value of our token. Here's an example:

```dart
import 'package:http/http.dart' as http;

String apiUrl = 'https://api.example.com';

Future<http.Response> makeAuthenticatedRequest(String endpoint, String token) {
  Uri url = Uri.parse('$apiUrl/$endpoint');
  
  return http.get(
    url,
    headers: {'Authorization': 'Bearer $token'},
  );
}
```

In the above example, we define a function `makeAuthenticatedRequest` that takes an `endpoint` and a `token` as parameters. It constructs the request URL by appending the `endpoint` to the base URL. Then, it makes a `GET` request to the constructed URL with the `Authorization` header set to the provided `token`.

### Step 4: Handling the Response

Once we've made the authenticated request, we need to handle the response. The response will contain the data returned by the API server. Here's an example of how to handle the response:

```dart
void fetchData(String token) {
  makeAuthenticatedRequest('data', token).then((response) {
    if (response.statusCode == 200) {
      // Successful response
      print(response.body);
    } else {
      // Error response
      print('Error: ${response.statusCode}');
    }
  }).catchError((error) {
    // Error occurred while making the request
    print('Error: $error');
  });
}
```

In the above example, we call the `makeAuthenticatedRequest` function and handle the response using a `.then` method. If the response status code is 200, we log the response body as successful. Otherwise, we log the error status code.

### Conclusion

In this blog post, we learned how to make authenticated requests with tokens using the `http` package in Flutter. We covered the steps to import the `http` package, obtain a token, configure authenticated requests, and handle the responses. Incorporating token-based authentication in your app allows you to securely communicate with APIs and access protected resources.

#flutter #httppackage