---
layout: post
title: "Deserializing JSON in Flutter with JSON Serializable"
description: " "
date: 2023-09-27
tags: [json, serialization]
comments: true
share: true
---

When working with APIs in Flutter, you often need to deserialize JSON responses into Dart objects. This can be a tedious task if you have to manually write the deserialization code for each object. Thankfully, the JSON Serializable package comes to the rescue.

JSON Serializable is a code generation library for Dart that automatically generates serialization and deserialization code for your Dart classes based on annotations. It simplifies the process of converting JSON data to Dart objects and vice versa.

## Getting Started

To use JSON Serializable in your Flutter project, you first need to add the `json_annotation` and `json_serializable` packages to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  json_annotation: ^4.4.0
  json_serializable: ^4.1.3
```

After adding the packages, run `flutter pub get` to fetch the dependencies.

## Creating the Model Class

Next, let's create a simple Dart class that represents the JSON data we want to deserialize. For example, consider a `User` class:

```dart
import 'package:json_annotation/json_annotation.dart';

part 'user.g.dart';

@JsonSerializable()
class User {
  final String name;
  final int age;

  User(this.name, this.age);

  factory User.fromJson(Map<String, dynamic> json) => _$UserFromJson(json);
  Map<String, dynamic> toJson() => _$UserToJson(this);
}
```

In the above code, we're using the `@JsonSerializable()` annotation from the `json_annotation` package to generate the serialization and deserialization code for our `User` class.

## Generating Code

To generate the necessary code, run the following command in your terminal:

```shell
flutter pub run build_runner build
```

This command generates the serialization and deserialization code based on the annotations in your Dart files. The generated code will be saved in a file called `*.g.dart`, where `*` represents the name of your original Dart file.

## Using the Generated Code

Once the code generation is complete, you can deserialize JSON data into Dart objects using the generated `fromJson` factory method. Here's an example:

```dart
import 'dart:convert';

void main() {
  String json = '{"name": "John Doe", "age": 25}';
  Map<String, dynamic> jsonData = jsonDecode(json);

  User user = User.fromJson(jsonData);

  print('Name: ${user.name}');
  print('Age: ${user.age}');
}
```

In the above code, we decode the JSON string using `jsonDecode` and pass the resulting `Map<String, dynamic>` to the `fromJson` factory method of the `User` class. We can then access the deserialized object properties like any regular Dart object.

To convert a Dart object back to JSON, use the `toJson` method:

```dart
User user = User('Jane Smith', 30);
String json = jsonEncode(user.toJson());
print(json);
```

## Conclusion

Deserializing JSON data in Flutter becomes much easier with the JSON Serializable package. By generating the serialization and deserialization code automatically, you can focus on building your app's logic rather than manually handling JSON parsing.

Remember to run the code generation command each time you modify your Dart classes annotated with `@JsonSerializable()`.

#flutter #json #serialization #deserialization