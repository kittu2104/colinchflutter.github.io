---
layout: post
title: "Serializing JSON with custom converters in Flutter"
description: " "
date: 2023-09-27
tags: [JSONSerialization]
comments: true
share: true
---

When working with network requests in Flutter, it's common to need to convert JSON data into Dart objects and vice versa. Flutter provides a powerful package called `json_serializable` which allows you to automatically generate the serialization code for your Dart classes. However, there might be cases where you need custom serialization logic for certain fields. In such scenarios, you can use custom converters to handle the serialization and deserialization process.

## Setting up the Environment ##

Before we dive into using custom converters, make sure you have the `json_serializable` package added to your `pubspec.yaml` file.

```
dependencies:
  flutter:
    sdk: flutter
  json_annotation: <latest_version>   # Add this line
  json_serializable: <latest_version> # Add this line
```

Then, run `flutter pub get` in your terminal to fetch the packages.

## Creating a Custom Converter ##

Assume you have a Dart class called `Person` with the following structure:

```dart
import 'package:json_annotation/json_annotation.dart';

part 'person.g.dart';

@JsonSerializable()
class Person {
  final String name;
  final DateTime birthDate;
  
  Person({
    required this.name,
    required this.birthDate,
  });

  factory Person.fromJson(Map<String, dynamic> json) => 
    _$PersonFromJson(json);
  
  Map<String, dynamic> toJson() => _$PersonToJson(this);
}
```

The `Person` class has two fields: `name` and `birthDate`. By default, the `json_serializable` package can handle serializing and deserializing most basic types like `String` and `DateTime`. However, if you have a custom type that is not natively supported, such as `DateTime`, you need to create a custom converter.

To create a custom converter, follow these steps:

1. Create a new class that extends `JsonConverter<T, Map<String, dynamic>>`, where `T` is the type you want to convert.
2. Implement the `fromJson` and `toJson` methods based on your custom serialization logic.

Here's an example of a custom `DateTime` converter:

```dart
class DateTimeConverter implements JsonConverter<DateTime, String> {
  const DateTimeConverter();

  @override
  DateTime fromJson(String json) {
    // Implement your custom deserialization logic here
    return DateTime.parse(json);
  }

  @override
  String toJson(DateTime object) {
    // Implement your custom serialization logic here
    return object.toIso8601String();
  }
}
```

## Wiring Up the Custom Converter ##

Once you have created the custom converter, you need to wire it up to the field in your `Person` class that requires custom serialization.

To do this, annotate the field with the `@JsonKey` annotation and specify the `fromJson` and `toJson` functions on the `fromJson` and `toJson` fields respectively.

```dart
@JsonSerializable()
class Person {
  final String name;
  
  @JsonKey(fromJson: _dateTimeFromJson, toJson: _dateTimeToJson)
  final DateTime birthDate;
  
  Person({
    required this.name,
    required this.birthDate,
  });

  factory Person.fromJson(Map<String, dynamic> json) => 
    _$PersonFromJson(json);
  
  Map<String, dynamic> toJson() => _$PersonToJson(this);
  
  static DateTime _dateTimeFromJson(String value) {
    return DateTime.parse(value);
  }
  
  static String _dateTimeToJson(DateTime value) {
    return value.toIso8601String();
  }
}
```

## Conclusion ##

By following the steps above, you can easily create and use custom converters with the `json_serializable` package in Flutter. These converters allow you to handle custom serialization and deserialization logic for fields in your Dart classes. This flexibility ensures you can easily work with complex JSON structures and custom data types in your Flutter applications.

#Flutter #JSONSerialization