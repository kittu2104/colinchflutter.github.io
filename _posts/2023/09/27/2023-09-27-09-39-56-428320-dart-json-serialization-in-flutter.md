---
layout: post
title: "Dart JSON serialization in Flutter"
description: " "
date: 2023-09-27
tags: [dart, json]
comments: true
share: true
---

Flutter is a popular framework for building cross-platform mobile applications. One of the key features of Flutter is its ability to work with JSON data. In this blog post, we will explore how to serialize and deserialize JSON data in Dart, the programming language used in Flutter.

## What is JSON Serialization?

JSON (JavaScript Object Notation) is a lightweight data interchange format that is used to transmit data between a server and a web application. JSON serialization is the process of converting JSON data into Dart objects, and vice versa.

## JSON Serialization in Dart

Dart provides a powerful and easy-to-use library for JSON serialization called `json_serializable`. This library automatically generates code for converting Dart objects to and from JSON, based on annotated classes.

To use `json_serializable`, we need to add it as a dependency in our `pubspec.yaml` file:
```yaml
dependencies:
  json_annotation: ^3.1.0
  json_serializable: ^4.1.3
```

Next, we need to create a Dart class that represents the structure of our JSON data. We can define the class fields using appropriate data types, such as `String`, `int`, `bool`, or even other custom classes.

For example, let's say we have the following JSON data representing a user:
```json
{
  "id": 1,
  "name": "John Doe",
  "email": "johndoe@example.com"
}
```

We can create a Dart class for the user data:
```dart
import 'package:json_annotation/json_annotation.dart';

part 'user.g.dart';

@JsonSerializable()
class User {
  int id;
  String name;
  String email;

  User();

  factory User.fromJson(Map<String, dynamic> json) => _$UserFromJson(json);
  Map<String, dynamic> toJson() => _$UserToJson(this);
}
```

In this example, we have used the `@JsonSerializable()` annotation to indicate that this class should be serialized. We also define a `factory` method for deserializing JSON data and a `toJson()` method for serializing the object back to JSON.

To generate the required serialization code, we need to run the following command in the project directory:
```bash
flutter packages pub run build_runner build
```

After running the command, the `user.g.dart` file will be generated, containing the necessary code for JSON serialization and deserialization.

Now, we can easily convert JSON data to a Dart object and vice versa:
```dart
import 'dart:convert';

void main() {
  String jsonStr = '{"id": 1, "name": "John Doe", "email": "johndoe@example.com"}';

  final user = User.fromJson(json.decode(jsonStr));
  print(user.name); // John Doe

  final jsonUser = user.toJson();
  print(json.encode(jsonUser)); // {"id":1,"name":"John Doe","email":"johndoe@example.com"}
}
```

By using the `json_serializable` library, we can handle JSON serialization and deserialization in Dart with ease, making it a breeze to work with JSON data in Flutter applications.

#flutter #dart #json #serialization