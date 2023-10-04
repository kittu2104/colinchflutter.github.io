---
layout: post
title: "Code generation for JSON serialization in Flutter"
description: " "
date: 2023-09-27
tags: [JSONSerialization]
comments: true
share: true
---

JSON (JavaScript Object Notation) is a widely used format for data interchange between a server and a client application. In Flutter, it is common to convert JSON data into Dart objects for easier manipulation and type safety. Manually writing the serialization and deserialization code for JSON can be a tedious and error-prone task. However, Flutter provides a convenient way to generate code for JSON serialization using a package called `json_serializable`.

## What is `json_serializable`?

`json_serializable` is a code generation library in Flutter that simplifies the process of converting JSON to Dart code and vice versa. It automatically generates the serialization and deserialization code based on annotated classes.

## Setting up `json_serializable`

To use `json_serializable` in your Flutter project, you need to add the following dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  json_annotation: ^4.0.1

dev_dependencies:
  build_runner: ^2.1.2
  json_serializable: ^4.1.2
```

After adding the dependencies, run the following command in your terminal to fetch the packages:

```bash
flutter packages get
```

## Generating Serialization Code

Once `json_serializable` is set up, you can start annotating your Dart classes with special annotations from the `json_annotation` package. Here's an example:

```dart
import 'package:json_annotation/json_annotation.dart';

part 'person.g.dart';

@JsonSerializable()
class Person {
  final String name;
  final int age;

  Person(this.name, this.age);

  factory Person.fromJson(Map<String, dynamic> json) => _$PersonFromJson(json);
  Map<String, dynamic> toJson() => _$PersonToJson(this);
}
```

In the above code, we use the `@JsonSerializable()` annotation on the `Person` class. This annotation tells the code generator to generate serialization and deserialization code for this class.

## Running the Code Generator

To generate the serialization code, run the following command in your terminal:

```bash
flutter packages pub run build_runner build
```

The code generator will scan your project for classes annotated with `@JsonSerializable()` and generate the corresponding serialization and deserialization code. The generated code will be placed in a file named `person.g.dart`.

## Using the Generated Code

After running the code generator, you can easily serialize and deserialize JSON using the generated code. Here's an example:

```dart
final json = '{"name": "John Doe", "age": 30}';
final person = Person.fromJson(jsonDecode(json));

print(person.name); // Output: John Doe
print(person.age); // Output: 30

final newPerson = Person('Jane Smith', 25);
final newJson = jsonEncode(newPerson.toJson());

print(newJson); // Output: {"name": "Jane Smith", "age": 25}
```

As you can see, we can effortlessly convert JSON data to Dart objects and vice versa using the generated serialization and deserialization code.

## Conclusion

`json_serializable` is a powerful package in Flutter that automates the process of generating code for JSON serialization and deserialization. By annotating classes with `@JsonSerializable()`, you can generate the serialization code with ease. This not only saves time but also reduces the chance of manual errors. It's a great tool to have in your Flutter development toolkit when working with JSON data. Give it a try and see how it simplifies your code! #Flutter #JSONSerialization