---
layout: post
title: "Mapping JSON keys to class properties in Flutter"
description: " "
date: 2023-09-27
tags: [json, serialization]
comments: true
share: true
---

One common task in mobile app development is mapping JSON data to class properties. In Flutter, we have the ability to easily parse JSON data and map it to our model classes. In this blog post, we will explore how to efficiently map JSON keys to class properties in Flutter using the `json_serializable` package.

## Introduction to `json_serializable` package

The `json_serializable` package is a code generator that helps us with JSON serialization and deserialization in Dart. It automatically generates the code needed to parse JSON data into Dart classes and vice versa.

To use the `json_serializable` package in your Flutter project, you need to add the following dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
    
dev_dependencies:
  build_runner: ^1.0.0
  json_annotation: ^3.0.0
  json_serializable: ^4.0.0
```

After adding the dependencies, run `flutter pub get` to fetch the packages.

## Creating the Model Class

Let's say we have a JSON response like this:

```json
{
  "name": "John Doe",
  "age": 25,
  "email": "johndoe@example.com"
}
```

We want to create a Dart class to represent this data. We can do this by creating a new file, e.g., `user_model.dart`, and defining our model class:

```dart
import 'package:json_annotation/json_annotation.dart';

part 'user_model.g.dart';

@JsonSerializable()
class UserModel {
  String name;
  int age;
  String email;

  UserModel({this.name, this.age, this.email});

  factory UserModel.fromJson(Map<String, dynamic> json) =>
      _$UserModelFromJson(json);

  Map<String, dynamic> toJson() => _$UserModelToJson(this);
}
```

Note that we annotate our class with `@JsonSerializable()` and use the `part` directive to include the generated code.

## Generating the Model Class

To generate the necessary code for JSON serialization/deserialization, we need to run the following command in the terminal:

```bash
flutter pub run build_runner build
```

This will generate the corresponding `.g.dart` file, which contains the generated code for the model class.

## Using the Model Class

Now that we have our `UserModel` class ready, we can easily map JSON data to our model by calling the `fromJson` factory method:

```dart
import 'dart:convert';

void main() {
  String jsonString = '{"name": "John Doe", "age": 25, "email": "johndoe@example.com"}';
  Map<String, dynamic> jsonMap = json.decode(jsonString);
  
  UserModel user = UserModel.fromJson(jsonMap);
  
  print(user.name);  // Output: John Doe
  print(user.age);   // Output: 25
  print(user.email); // Output: johndoe@example.com
}
```

Similarly, we can convert our model class back to JSON by calling the `toJson` method:

```dart
UserModel user = UserModel(name: "John Doe", age: 25, email: "johndoe@example.com");

String jsonString = json.encode(user.toJson());
print(jsonString); // Output: {"name":"John Doe","age":25,"email":"johndoe@example.com"}
```

## Conclusion

Using the `json_serializable` package in Flutter, we can easily map JSON keys to class properties. This allows us to parse JSON data into Dart objects and serialize our objects back to JSON. This approach helps us save time and write cleaner, more maintainable code.

#flutter #json #serialization #deserialization