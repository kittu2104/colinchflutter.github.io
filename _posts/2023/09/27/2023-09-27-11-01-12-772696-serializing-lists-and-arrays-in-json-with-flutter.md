---
layout: post
title: "Serializing lists and arrays in JSON with Flutter"
description: " "
date: 2023-09-27
tags: [json]
comments: true
share: true
---

Flutter is a cross-platform development framework that allows you to build native mobile apps for iOS and Android using a single codebase. It provides various tools and libraries to make app development easier and more efficient.

One common task in mobile app development is serializing data to JSON format. JSON (JavaScript Object Notation) is a lightweight data-interchange format that is easy for humans to read and write, and easy for machines to parse and generate.

In this blog post, we will learn how to serialize lists and arrays in JSON format using Flutter.

## Step 1: Import the required packages

To serialize lists and arrays in JSON format, we need to import the `dart:convert` package. Add the following import statement at the top of your Flutter file:

```dart
import 'dart:convert';
```

## Step 2: Define the data structure

Next, we need to define the data structure that we want to serialize. For example, let's say we have a `Person` class with `name` and `age` properties:

```dart
class Person {
  final String name;
  final int age;

  Person({required this.name, required this.age});
}
```

## Step 3: Serialize the data to JSON

To serialize the `Person` objects to JSON format, we can make use of the `jsonEncode()` function from the `dart:convert` package. Here's how you can do it:

```dart
List<Person> persons = [
  Person(name: "John", age: 25),
  Person(name: "Sarah", age: 28),
  Person(name: "Mike", age: 30),
];

String json = jsonEncode(persons);
print(json);
```

The `jsonEncode()` function takes an object and converts it to a JSON-serialized string representation. In this example, we pass the `persons` list to the `jsonEncode()` function, which will convert it to a JSON string.

## Step 4: Deserialize the JSON data

To deserialize the JSON data back to a list of `Person` objects, we can use the `jsonDecode()` function from the `dart:convert` package. Here's how you can do it:

```dart
String json = '[{"name":"John","age":25},{"name":"Sarah","age":28},{"name":"Mike","age":30}]';

List<dynamic> jsonList = jsonDecode(json);

List<Person> persons = jsonList.map((json) => Person(name: json['name'], age: json['age'])).toList();

print(persons);
```

In this example, we pass the JSON string to the `jsonDecode()` function, which returns a `List<dynamic>` representation of the JSON data. We then use the `map()` function to convert each JSON object to a `Person` object, and finally, we use the `toList()` function to convert the `Iterable` to a `List<Person>`.

## Conclusion

Serializing lists and arrays in JSON format is a common task in Flutter app development. By following the steps outlined in this blog post, you can easily serialize and deserialize your data to JSON format using the `dart:convert` package. This can be useful when working with APIs or when persisting data in a local database.

Remember to import the `dart:convert` package, define your data structure, and use the `jsonEncode()` and `jsonDecode()` functions to serialize and deserialize your data. Happy coding!

#flutter #json