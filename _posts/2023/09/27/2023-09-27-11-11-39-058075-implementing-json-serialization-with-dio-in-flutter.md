---
layout: post
title: "Implementing JSON serialization with dio in Flutter"
description: " "
date: 2023-09-27
tags: [Flutter, JSON]
comments: true
share: true
---

In this blog post, we will explore how to perform JSON serialization with Dio in a Flutter application. Serialization is the process of converting objects into a format that can be stored or transmitted. In Flutter, we often need to serialize and deserialize JSON data when working with APIs. Dio is a powerful HTTP client for Dart that makes working with APIs easier. Let's get started!

## Installing Dio

To use Dio in your Flutter project, you need to add the `dio` package as a dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  dio: ^4.0.0
```

After adding the dependency, run `flutter pub get` to fetch the package.

## Creating a Model Class

Before we can serialize and deserialize JSON data, we need to define a model class that represents the JSON structure. For example, let's say we have an API that returns a list of user data in JSON format. We can create a `User` class to represent each user:

```dart
class User {
  final int id;
  final String name;
  final String email;

  User({required this.id, required this.name, required this.email});

  factory User.fromJson(Map<String, dynamic> json) {
    return User(
      id: json['id'],
      name: json['name'],
      email: json['email'],
    );
  }

  Map<String, dynamic> toJson() {
    return {
      'id': id,
      'name': name,
      'email': email,
    };
  }
}
```

In the `User` class, we define the properties `id`, `name`, and `email`. We also create a factory method `fromJson` to create a `User` object from the JSON data received from the API. Additionally, we define a `toJson` method to convert a `User` object into a JSON object.

## Deserializing JSON Data

With the `User` model class ready, we can now use Dio to fetch and deserialize JSON data. To deserialize the JSON data, we can utilize the `fromJson` factory method defined in the `User` class. Here's an example of how to perform a GET request and deserialize the JSON data using Dio:

```dart
import 'package:dio/dio.dart';

void fetchUsers() async {
  try {
    final response = await Dio().get('https://api.example.com/users');
    final List<dynamic> jsonList = response.data;
    final List<User> users = jsonList.map((json) => User.fromJson(json)).toList();
    
    // Now we have a list of User objects
    for (User user in users) {
      print('${user.name}: ${user.email}');
    }
  } catch (e) {
    print('Error fetching users: $e');
  }
}
```

In the code above, we use the `Dio` HTTP client to perform a GET request to the API endpoint that returns the list of users as JSON data. We then convert the received JSON data into a list of `User` objects using the `fromJson` factory method. Finally, we can access the user properties and perform any necessary operations.

## Serializing JSON Data

To send JSON data to an API, we need to convert the `User` objects into a JSON format. We can achieve this by using the `toJson` method defined in the `User` class. Here's an example of how to perform a POST request and serialize the `User` object using Dio:

```dart
import 'package:dio/dio.dart';

void createUser(User user) async {
  try {
    final response = await Dio().post('https://api.example.com/users', data: user.toJson());
    print('User created successfully with ID: ${response.data['id']}');
  } catch (e) {
    print('Error creating user: $e');
  }
}
```

In the code above, we use the `Dio` HTTP client to perform a POST request to the API endpoint for creating a new user. We pass the serialized `User` object in the `data` parameter using the `toJson` method. After the request is successful, we can access the response data, including the ID of the created user.

## Conclusion

In this blog post, we have learned how to perform JSON serialization and deserialization with Dio in a Flutter application. We created a model class, `User`, to represent the JSON data structure and implemented the necessary methods for serialization and deserialization. With Dio, we can easily fetch JSON data from APIs, deserialize it into model objects, and send serialized objects back to APIs. This allows for seamless integration with JSON-based APIs in Flutter applications.

#Flutter #Dio #JSON #Serialization #Deserialization