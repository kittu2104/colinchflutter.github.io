---
layout: post
title: "Handling different data types in JSON serialization with Flutter"
description: " "
date: 2023-09-27
tags: [JSON]
comments: true
share: true
---

JSON (JavaScript Object Notation) is a popular format used for data exchange between a client and a server. In Flutter, you often need to serialize and deserialize data to and from JSON format. While this process is straightforward for simple types like strings and numbers, it can be more challenging when dealing with complex data structures or custom classes.

In this blog post, we will explore how to handle different data types in JSON serialization with Flutter. We will cover the built-in JSON serialization mechanisms provided by the Flutter framework as well as third-party packages that can simplify the process.

## Built-in JSON Serialization in Flutter

Flutter provides two built-in ways to handle JSON serialization: `dart:convert` and code generation with `json_serializable`.

### dart:convert

The `dart:convert` library included with Flutter provides a straightforward way to serialize and deserialize JSON data using the `json` class. 

To serialize an object to JSON, you can use the `json.encode()` method, passing in the object you want to convert. Here's an example:

```dart
import 'dart:convert';

// Serialize an object to JSON
var object = {
  'name': 'John',
  'age': 30,
  'isStudent': true
};

var jsonString = json.encode(object);
print(jsonString); // {"name":"John","age":30,"isStudent":true}
```

To deserialize JSON data back into an object, you can use the `json.decode()` method. Here's an example:

```dart
import 'dart:convert';

// Deserialize JSON to an object
var jsonString = '{"name":"John","age":30,"isStudent":true}';

var object = json.decode(jsonString);
print(object['name']); // John
print(object['age']); // 30
print(object['isStudent']); // true
```

### json_serializable

`json_serializable` is a code generation package that simplifies JSON serialization with Flutter. It generates serialization code for your classes at compile-time, reducing the overhead of runtime reflection.

To use `json_serializable`, you need to define your data classes and annotate them with the `@JsonSerializable()` decorator. Here's an example:

```dart
import 'package:json_annotation/json_annotation.dart';

part 'user.g.dart';

@JsonSerializable()
class User {
  final String name;
  final int age;
  final bool isStudent;

  User({this.name, this.age, this.isStudent});

  factory User.fromJson(Map<String, dynamic> json) => _$UserFromJson(json);
  Map<String, dynamic> toJson() => _$UserToJson(this);
}
```

To generate the serialization code, you run the build_runner command:

```bash
flutter packages pub run build_runner build
```

This generates the necessary serialization code (e.g., `user.g.dart`) which can be used to serialize and deserialize instances of the `User` class.

## Third-Party JSON Serialization Packages

Apart from the built-in options, there are several third-party packages available for JSON serialization in Flutter that offer additional features and flexibility.

### json_serializable_any

`json_serializable_any` is a package that provides a flexible way to serialize and deserialize JSON data with any structure. It allows you to define custom serialization and deserialization logic for complex types.

To use `json_serializable_any`, you need to annotate your custom class with the `@JsonConverter()` decorator and provide the necessary serialization and deserialization functions. Here's an example:

```dart
import 'package:json_annotation/json_annotation.dart';
import 'package:json_serializable_any/json_serializable_any.dart';

part 'custom_class.g.dart';

@JsonSerializable()
@JsonConverter(fromJson: fromJsonCustomClass, toJson: toJsonCustomClass)
class CustomClass {
  final String property1;
  final int property2;

  CustomClass({this.property1, this.property2});

  static CustomClass fromJsonCustomClass(Map<String, dynamic> json) {
    // Custom deserialization logic here
    return CustomClass(
        property1: json['property1'],
        property2: json['property2'],
    );
  }

  static Map<String, dynamic> toJsonCustomClass(CustomClass instance) {
    // Custom serialization logic here
    return {
      'property1': instance.property1,
      'property2': instance.property2,
    };
  }
}
```

### json_annotation_mapping

`json_annotation_mapping` is another package that provides a convenient way to control how objects are serialized and deserialized from JSON.

With `json_annotation_mapping`, you can annotate your class fields with `@JsonKey()` to specify custom mappings. Here's an example:

```dart
import 'package:json_annotation/json_annotation.dart';
import 'package:json_annotation_mapping/json_annotation_mapping.dart';

part 'custom_class.g.dart';

@JsonSerializable()
class CustomClass {
  @JsonKey(name: 'property_one')
  final String property1;

  @JsonKey(name: 'property_two')
  final int property2;

  CustomClass({this.property1, this.property2});

  factory CustomClass.fromJson(Map<String, dynamic> json) => _$CustomClassFromJson(json);
  Map<String, dynamic> toJson() => _$CustomClassToJson(this);
}
```

In this example, the `property1` field will be mapped to the `property_one` key in the JSON, and the `property2` field will be mapped to the `property_two` key.

## Conclusion

Handling different data types in JSON serialization is an essential skill when working with data exchange in Flutter. The built-in `dart:convert` library and `json_serializable` package provide convenient options for most use cases, while third-party packages like `json_serializable_any` and `json_annotation_mapping` offer more flexibility and control.

By understanding these different options and choosing the one that best fits your project's needs, you can efficiently serialize and deserialize JSON data with ease in your Flutter applications.

#Flutter #JSON #Serialization