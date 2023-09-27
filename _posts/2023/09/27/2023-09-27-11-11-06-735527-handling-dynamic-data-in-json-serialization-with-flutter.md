---
layout: post
title: "Handling dynamic data in JSON serialization with Flutter"
description: " "
date: 2023-09-27
tags: [JSONserialization]
comments: true
share: true
---

In any Flutter app, it is common to deal with dynamic data that needs to be serialized and deserialized from JSON. JSON (JavaScript Object Notation) is a popular data interchange format often used for transferring data between a server and a client. 

Flutter provides a convenient way to work with JSON through its serialization/deserialization library called `json_serializable`. This library simplifies the process of converting Dart objects to JSON and vice versa.

## Serializing Dart Objects to JSON

To serialize a Dart object to JSON, you need to annotate the class with `@JsonSerializable` and specify the fields that need to be included in the JSON representation. Here's an example of a `User` class:

```dart
import 'package:json_annotation/json_annotation.dart';

part 'user.g.dart';

@JsonSerializable()
class User {
  final String name;
  final int age;

  User({required this.name, required this.age});

  factory User.fromJson(Map<String, dynamic> json) => _$UserFromJson(json);
  
  Map<String, dynamic> toJson() => _$UserToJson(this);
}
```

In the above example, we have a `User` class with two fields: `name` and `age`. The `@JsonSerializable` annotation indicates that this class can be serialized to JSON. The class also includes factory methods `fromJson` and `toJson`, which are generated automatically by the `json_serializable` package.

Next, you need to generate the serialization code by running the following command in the terminal:

```shell
flutter pub run build_runner build
```

This command generates the `user.g.dart` file, which contains the necessary serialization code.

To serialize a `User` object to JSON, you can simply call the `toJson` method:

```dart
User user = User(name: 'John Doe', age: 25);
String jsonString = user.toJson();
```

## Deserializing JSON to Dart Objects

Similarly, to deserialize JSON to Dart objects, you need to provide a factory method called `fromJson` to create an instance of the object from a JSON map. In the previous example, the `fromJson` factory method is already defined:

```dart
factory User.fromJson(Map<String, dynamic> json) => _$UserFromJson(json);
```

To deserialize a JSON string to a `User` object, you can use the `fromJson` method:

```dart
String jsonString = '{"name":"John Doe","age":25}';
User user = User.fromJson(jsonDecode(jsonString));
```

In the above code, we use `jsonDecode` to convert the JSON string to a `Map`, and then pass it to the `fromJson` method to create a `User` object.

#flutter #JSONserialization