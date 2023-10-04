---
layout: post
title: "JSON serialization in Flutter using built_value library"
description: " "
date: 2023-09-27
tags: [JSONSerialization]
comments: true
share: true
---

Flutter is a cross-platform framework for building mobile applications. When working with APIs, it is common to interact with data in JSON format. JSON serialization is the process of converting objects into a JSON string to be sent over the network, and JSON deserialization is the process of converting a JSON string back into objects.

Flutter provides several libraries for JSON serialization, and one popular choice is the `built_value` library. `built_value` is a code generation library that helps eliminate boilerplate code when working with immutable objects.

In this blog post, we will walk through the process of integrating `built_value` into a Flutter project and using it for JSON serialization.

## Step 1: Add Dependencies

Begin by adding the required dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  built_value: ^8.1.0
  built_value_generator: ^8.1.0
  built_collection: ^5.0.0
  json_annotation: ^4.5.0
```

Run `flutter packages get` to fetch the newly added dependencies.

## Step 2: Define Model Classes

Next, define the model classes that represent your JSON data. For example, let's say we have a `User` class with a `name` and `email` property:

```dart
import 'package:built_value/built_value.dart';
import 'package:built_value/serializer.dart';

part 'user.g.dart';

abstract class User implements Built<User, UserBuilder> {
  String get name;
  String get email;

  User._();

  factory User([void Function(UserBuilder) updates]) = _$User;

  static Serializer<User> get serializer => _$userSerializer;
}
```

Note the `part` statement and the `_$User` class that is automatically generated when you run the code generation step.

## Step 3: Generate Serialization Code

To generate the serialization code, you need to run the build runner. Use the following command in your terminal:

```bash
flutter packages pub run build_runner build
```

This command generates the necessary code in the background based on the annotations and constructs you have used.

## Step 4: Serializing and Deserializing

Now you can use the generated code to serialize and deserialize JSON data. Here's an example of how to do it with our `User` class:

```dart
import 'dart:convert';

User userFromJson(String jsonString) {
  final parsed = json.decode(jsonString);
  User user = standardSerializers.deserializeWith(User.serializer, parsed);
  return user;
}

String userToJson(User user) {
  Map<String, dynamic> jsonMap = standardSerializers.serializeWith(User.serializer, user);
  return json.encode(jsonMap);
}
```

Here, `standardSerializers` is provided by the `built_value` library and is used to serialize and deserialize objects.

## Conclusion

In this blog post, we have explored how to use the `built_value` library for JSON serialization in a Flutter project. By leveraging code generation, we can eliminate tedious and error-prone boilerplate code when working with JSON data.

By following the steps outlined above, you can easily integrate `built_value` and take advantage of its features to streamline your JSON serialization and deserialization process in Flutter.

#Flutter #JSONSerialization