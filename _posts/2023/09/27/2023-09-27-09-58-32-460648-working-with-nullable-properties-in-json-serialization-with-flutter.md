---
layout: post
title: "Working with nullable properties in JSON serialization with Flutter"
description: " "
date: 2023-09-27
tags: [FlutterDevelopers, JSONSerialization]
comments: true
share: true
---

When working with JSON data in Flutter, it's common to come across nullable properties. Nullable properties are those that can have a null value instead of a specific data type.

In this blog post, we will discuss how to handle nullable properties when serializing and deserializing JSON data in Flutter.

## Serializing Nullable Properties

When serializing JSON data, we need to handle nullable properties carefully. By default, the `jsonEncode()` function provided by the `dart:convert` library in Flutter does not handle nullable properties properly. If a nullable property has a null value, it will be treated as an absent property in the encoded JSON string.

To ensure that nullable properties are included with a null value, we can use the `json.encode()` function from the `json_annotation` package. This package provides annotations and code generation for JSON serialization in Dart. It also handles nullable properties correctly.

Here's an example of serializing an object with nullable properties using the `json.encode()` function:

```dart
import 'dart:convert';
import 'package:json_annotation/json_annotation.dart';

part 'example_model.g.dart';

@JsonSerializable()
class ExampleModel {
  String? name;
  int? age;

  ExampleModel(this.name, this.age);

  factory ExampleModel.fromJson(Map<String, dynamic> json) =>
      _$ExampleModelFromJson(json);
  Map<String, dynamic> toJson() => _$ExampleModelToJson(this);
}

void main() {
  ExampleModel model = ExampleModel('John Doe', null);
  String jsonString = json.encode(model);
  print(jsonString); // {"name":"John Doe","age":null}
}
```

In the above example, the `name` property is a non-nullable string, while the `age` property is a nullable integer. When serializing the `ExampleModel` instance, the `json.encode()` function from the `json_annotation` package correctly includes the `age` property in the JSON string with a null value.

## Deserializing Nullable Properties

When deserializing JSON data with nullable properties, we need to handle them accordingly. The `jsonDecode()` function provided by the `dart:convert` library in Flutter treats absent properties as null values for nullable properties.

To handle nullable properties in the deserialization process, we can manually check for null values and assign them accordingly.

Here's an example of deserializing JSON data with nullable properties in Flutter:

```dart
import 'dart:convert';

class ExampleModel {
  String? name;
  int? age;

  ExampleModel(this.name, this.age);
}

void main() {
  String jsonString = '{"name":"John Doe","age":null}';
  Map<String, dynamic> jsonData = jsonDecode(jsonString);

  ExampleModel model = ExampleModel(
    jsonData['name'] as String?,
    jsonData['age'] as int?,
  );

  print(model.name); // John Doe
  print(model.age); // null
}
```

In the above example, we manually cast the values to the nullable types when assigning them. This ensures that nullable properties are assigned properly, even if they have null values.

## Conclusion

When working with nullable properties in JSON serialization and deserialization with Flutter, it's important to be mindful of how they are handled. By using the `json.encode()` function from the `json_annotation` package for serialization and manually checking for null values during deserialization, we can confidently work with nullable properties in our Flutter applications.

#FlutterDevelopers #JSONSerialization