---
layout: post
title: "Serializing JSON data from a REST API in Flutter"
description: " "
date: 2023-09-27
tags: [restapi, json]
comments: true
share: true
---

Flutter is a popular framework for building cross-platform mobile applications. When working with REST APIs, it is common to receive data in JSON format. In Flutter, you can easily serialize JSON data into Dart objects using the built-in `dart:convert` library.

## Step 1: Import the required libraries

First, you need to import the necessary libraries for working with JSON and making HTTP requests. Add the following import statements at the top of your Dart file:

```dart
import 'dart:convert';
import 'package:http/http.dart' as http;
```

## Step 2: Create a model class

Next, create a model class representing the structure of the JSON data. This model class is used to parse the JSON response into Dart objects. You can define the necessary properties and methods in this class. For example:

```dart
class User {
  final String name;
  final String email;

  User({required this.name, required this.email});

  factory User.fromJson(Map<String, dynamic> json) {
    return User(
      name: json['name'],
      email: json['email'],
    );
  }
}
```

In this example, the `User` class has two properties - `name` and `email`. The `fromJson` factory method is responsible for converting the JSON data into a `User` object.

## Step 3: Fetch JSON data from a REST API

To fetch JSON data from a REST API, you can use the `http` package in Flutter. Here's an example of how to make an HTTP GET request and parse the JSON response:

```dart
Future<User> fetchUser() async {
  final response = await http.get(Uri.parse('https://api.example.com/user'));
  
  if (response.statusCode == 200) {
    // If the request is successful, parse the JSON response
    return User.fromJson(json.decode(response.body));
  } else {
    // If the request fails, throw an exception or handle the error
    throw Exception('Failed to fetch user data');
  }
}
```

In this code snippet, we call the `get` method of the `http` package to fetch data from the specified URL. If the response is successful (status code 200), we parse the JSON using the `fromJson` factory method of the `User` class. If the request fails, we throw an exception or handle the error accordingly.

## Step 4: Usage

Now, you can use the `fetchUser` method to obtain a `User` object:

```dart
fetchUser().then((user) {
  print('Name: ${user.name}');
  print('Email: ${user.email}');
}).catchError((error) {
  print('Error: $error');
});
```

In this example, we print the name and email of the user obtained from the REST API response. If an error occurs during the process, it will be caught and printed.

## Conclusion

Serializing JSON data from a REST API in Flutter is made easy with the help of the `dart:convert` library. By creating a model class and utilizing the `fromJson` method, you can seamlessly convert JSON responses into Dart objects. This allows for convenient data manipulation within your Flutter app. 

#flutter #restapi #json #serialization