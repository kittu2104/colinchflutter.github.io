---
layout: post
title: "Using annotations for JSON serialization in Flutter"
description: " "
date: 2023-09-27
tags: [JSON, serialization]
comments: true
share: true
---

When working with APIs and data serialization in Flutter, it is common to need to convert JSON data into Dart objects and vice versa. Flutter provides a convenient way to handle this using annotations to define how the serialization should be done.

## Step 1: Add the `json_annotation` Dependency

To use annotations for JSON serialization, we need to first add the `json_annotation` package as a dependency in the `pubspec.yaml` file of your Flutter project.

```yaml
dependencies:
  flutter:
    sdk: flutter
  json_annotation: ^4.4.0
```

After adding the dependency, run `flutter pub get` to fetch the package.

## Step 2: Annotate Your Dart Classes

Next, you need to annotate your Dart classes that you want to serialize and deserialize from JSON. For this, you can use the `@JsonSerializable` annotation from the `json_annotation` package.

Here's an example of a Dart class that represents a `User`:

```dart
import 'package:json_annotation/json_annotation.dart';

part 'user.g.dart';

@JsonSerializable()
class User {
  final String name;
  final int age;

  User(this.name, this.age);

  factory User.fromJson(Map<String, dynamic> json) =>
      _$UserFromJson(json);

  Map<String, dynamic> toJson() => _$UserToJson(this);
}
```

In this example, the `@JsonSerializable` annotation is used to denote that the `User` class needs to be serialized and deserialized. 

The `fromJson` factory method and `toJson` method are automatically generated for you by the build system. These methods handle the conversion between JSON and Dart object.

## Step 3: Generate Serialization Code

After annotating the classes, you need to generate the serialization code using the build runner tool. To do this, run the following command:

```bash
flutter pub run build_runner build
```

This command will generate the necessary serialization code for your annotated classes. Generated files will be placed in the same location as your original Dart files and have a `.g.dart` extension.

## Step 4: Using Serialization

Now that your classes are annotated and the serialization code has been generated, you can easily convert your Dart objects to JSON and vice versa.

To convert a JSON string to a Dart object:

```dart
String jsonString = '{"name": "John", "age": 25}';
User user = User.fromJson(jsonDecode(jsonString));
```

To convert a Dart object to JSON:

```dart
User user = User('John', 25);
Map<String, dynamic> json = user.toJson();
String jsonString = jsonEncode(json);
```

By using annotations and the generated serialization code, handling JSON serialization and deserialization becomes much simpler and less error-prone in Flutter.

#flutter #JSON #serialization