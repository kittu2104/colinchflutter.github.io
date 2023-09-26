---
layout: post
title: "How to handle Cross-Origin Resource Sharing (CORS) using the http package in Flutter?"
description: " "
date: 2023-09-27
tags: [tags]
comments: true
share: true
---

When building mobile applications with Flutter, you may encounter situations where you need to make HTTP requests to external APIs that are hosted on different domains. However, due to security restrictions imposed by browsers, these requests may be blocked by Cross-Origin Resource Sharing (CORS) policies.

Fortunately, Flutter provides the `http` package, which allows you to make HTTP requests and includes options to handle CORS issues. Here's how you can handle CORS using the `http` package in Flutter:

1. ## Import the necessary packages

   ```dart
   import 'package:http/http.dart' as http;
   ```

2. ## Make the HTTP request

   To make an HTTP request, you can use the `http.get()` or `http.post()` methods from the `http` package. For example, let's make a GET request to an external API:

   ```dart
   Future<void> makeRequest() async {
     final url = 'https://api.example.com/data';
     final response = await http.get(Uri.parse(url));
     
     // Handle the response
     if (response.statusCode == 200) {
       // Request was successful
       final responseBody = response.body;
       // Continue processing the response
     } else {
       // Request failed
       final errorMessage = response.body;
       // Handle the error
     }
   }
   ```

3. ## Add CORS headers to the request

   If the server you are making the request to requires additional CORS headers, you can include them in the request headers using the `headers` parameter. For example:

   ```dart
   Future<void> makeRequest() async {
     final url = 'https://api.example.com/data';
     final headers = {
       'Access-Control-Allow-Origin': '*',  // Replace '*' with the allowed origin
       'Access-Control-Allow-Methods': 'GET, POST, OPTIONS',  // Add allowed methods
       // Add other required CORS headers if needed
     };
     final response = await http.get(Uri.parse(url), headers: headers);
     
     // Handle the response
   }
   ```

   It's important to note that the server itself must be configured to allow the specified headers.

4. ## Handle CORS-related errors

   If the server does not include the necessary CORS headers or does not allow the requested origin, it will return a CORS-related error. You can handle these errors in the `else` block of the response handling code. For example:

   ```dart
   if (response.statusCode == 200) {
     // Request was successful
     final responseBody = response.body;
     // Continue processing the response
   } else {
     // Request failed
     if (response.statusCode == 403) {
       // Handle CORS-related error
       final errorMessage = 'CORS Error: ${response.statusCode}';
       // Display an error message to the user
     } else {
       // Handle other HTTP errors
       final errorMessage = response.body;
       // Display an error message to the user
     }
   }
   ```

By following these steps, you can handle Cross-Origin Resource Sharing (CORS) issues when making HTTP requests using the `http` package in your Flutter applications. Remember to ensure that the server you are making requests to allows the required CORS headers for a successful response.

#tags: `Flutter` `CORS`