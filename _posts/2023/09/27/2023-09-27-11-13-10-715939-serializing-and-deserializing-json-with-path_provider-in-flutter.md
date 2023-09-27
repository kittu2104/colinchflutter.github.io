---
layout: post
title: "Serializing and deserializing JSON with path_provider in Flutter"
description: " "
date: 2023-09-27
tags: [JSONSerialization, Deserialization]
comments: true
share: true
---

JSON (JavaScript Object Notation) is a widely used data format for exchanging data between a server and a client. In Flutter, you can easily serialize and deserialize JSON using the `dart:convert` package. Additionally, the `path_provider` package allows you to access the device's file system to save and retrieve JSON data.

In this article, we will discuss how to serialize and deserialize JSON using the `dart:convert` package, and how to use the `path_provider` package to store and retrieve JSON data in Flutter.

## Serializing JSON

Serialization is the process of converting an object into a JSON format. In Flutter, you can serialize JSON using the `jsonEncode` method provided by the `dart:convert` package.

Here's an example of how to serialize an object to JSON:

```dart
import 'dart:convert';

class User {
  String name;
  int age;

  User({required this.name, required this.age});

  Map<String, dynamic> toJson() {
    return {
      'name': name,
      'age': age,
    };
  }
}

void main() {
  User user = User(name: 'John Doe', age: 30);
  String jsonUser = jsonEncode(user.toJson());

  print(jsonUser);
}
```

In the above example, we define a `User` class with two properties: `name` and `age`. The `toJson` method returns a `Map` representation of the object, which is then encoded using `jsonEncode` to produce the JSON string.

## Deserializing JSON

Deserialization is the process of converting a JSON string back into an object. In Flutter, you can deserialize JSON using the `jsonDecode` method provided by the `dart:convert` package.

Here's an example of how to deserialize a JSON string into an object:

```dart
import 'dart:convert';

class User {
  String name;
  int age;

  User({required this.name, required this.age});

  factory User.fromJson(Map<String, dynamic> json) {
    return User(
      name: json['name'],
      age: json['age'],
    );
  }
}

void main() {
  String jsonUser = '{"name": "John Doe", "age": 30}';
  Map<String, dynamic> userData = jsonDecode(jsonUser);

  User user = User.fromJson(userData);

  print(user.name);
  print(user.age);
}
```

In the above example, we define a `User` class with a factory method `fromJson` that accepts a `Map` and creates a new `User` object from it. The `jsonDecode` function is used to parse the JSON string into a `Map`, which is then passed to the `fromJson` factory method to create the `User` object.

## Storing and Retrieving JSON Data

To store and retrieve JSON data in Flutter, we can use the `path_provider` package to access the device's file system. The `getApplicationDocumentsDirectory` method provided by the package gives us the directory path where we can store application-specific data.

Here's an example of how to store and retrieve JSON data using the `path_provider` package:

```dart
import 'dart:convert';
import 'dart:io';
import 'package:path_provider/path_provider.dart';

class User {
  String name;
  int age;

  User({required this.name, required this.age});

  Map<String, dynamic> toJson() {
    return {
      'name': name,
      'age': age,
    };
  }
}

void saveUser(User user) async {
  Directory directory = await getApplicationDocumentsDirectory();
  File file = File('${directory.path}/user.json');
  String jsonData = jsonEncode(user.toJson());
  await file.writeAsString(jsonData);
}

Future<User?> getUser() async {
  Directory directory = await getApplicationDocumentsDirectory();
  File file = File('${directory.path}/user.json');

  if (file.existsSync()) {
    String jsonData = await file.readAsString();
    Map<String, dynamic> userData = jsonDecode(jsonData);
    return User.fromJson(userData);
  } else {
    return null;
  }
}
```

In the above example, we define the `saveUser` and `getUser` functions. The `saveUser` function serializes the `User` object to JSON, gets the application documents directory using `getApplicationDocumentsDirectory`, creates a `File` with the file path `'user.json'`, and writes the JSON data to the file.

The `getUser` function retrieves the application documents directory, checks if the file exists, reads the JSON data from the file, and deserializes it into a `User` object.

By combining the serialization and deserialization techniques with the file system access provided by the `path_provider` package, you can easily store and retrieve JSON data in Flutter.

#flutter #JSONSerialization #Deserialization