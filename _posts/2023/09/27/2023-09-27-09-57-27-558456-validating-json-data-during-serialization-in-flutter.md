---
layout: post
title: "Validating JSON data during serialization in Flutter"
description: " "
date: 2023-09-27
tags: []
comments: true
share: true
---

When working with JSON data in Flutter, it is important to ensure that the data being serialized and deserialized is valid. This helps in preventing runtime errors and enhances the overall stability of the application. In this blog post, we will explore how to validate JSON data during serialization in Flutter.

## JSON Serialization in Flutter

Flutter provides a convenient way to serialize and deserialize JSON data using the `json_serializable` package. This package automatically generates the serialization code based on the annotations we provide. However, it does not perform any validation on the JSON data by default.

## JSON Schema Validation

To validate JSON data during serialization in Flutter, we can make use of the `json_annotation` package along with the `json_serializable` package. The `json_annotation` package allows us to define JSON Schema definitions for our data classes.

Here's an example of how to validate JSON data using JSON Schema:

1. First, we need to add the `json_annotation` package to our `pubspec.yaml` file:
```yaml
dependencies:
  flutter:
    sdk: flutter

  json_annotation: ^4.0.0
  json_serializable: ^4.0.0
```

2. Next, let's define a data class `Person` with some properties:
```dart
import 'package:json_annotation/json_annotation.dart';

part 'person.g.dart';

@JsonSerializable()
class Person {
  @JsonKey(required: true)
  final String name;

  @JsonKey(required: true)
  final int age;

  Person({required this.name, required this.age});

  factory Person.fromJson(Map<String, dynamic> json) => _$PersonFromJson(json);
  Map<String, dynamic> toJson() => _$PersonToJson(this);
}
```

3. Run the following command to generate the serialization code:
```bash
flutter pub run build_runner build
```

4. Now, we can validate the JSON data during serialization by adding JSON Schema annotations to our `Person` class:
```dart
@JsonSerializable()
class Person {
  @JsonKey(required: true)
  final String name;

  @JsonKey(required: true)
  final int age;

  Person({required this.name, required this.age});

  factory Person.fromJson(Map<String, dynamic> json) {
    validateJson<Person>(json);
    return _$PersonFromJson(json);
  }

  Map<String, dynamic> toJson() {
    final json = _$PersonToJson(this);
    validateJson<Person>(json);
    return json;
  }
}

void validateJson<T>(Map<String, dynamic> json) {
  final instance = _$_$_$TFromJson(json);
  final validationResult = instance.validate();
  if (validationResult != null) {
    throw FormatException(validationResult.toString());
  }
}
```

By adding the `validateJson` function to our class, we can catch any validation errors during serialization and throw a `FormatException` with the error message.

## Conclusion

Validating JSON data during serialization in Flutter is essential to ensure that the data being processed is valid and maintain application stability. By making use of the `json_annotation` and `json_serializable` packages, we can easily add JSON Schema validation to our data classes.