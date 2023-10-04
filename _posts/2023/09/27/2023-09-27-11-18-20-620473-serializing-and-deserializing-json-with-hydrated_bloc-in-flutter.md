---
layout: post
title: "Serializing and deserializing JSON with hydrated_bloc in Flutter"
description: " "
date: 2023-09-27
tags: [JSON]
comments: true
share: true
---

JSON (JavaScript Object Notation) is a popular format for storing and exchanging data. When working with Flutter and using the hydrated_bloc package, you may need to serialize and deserialize JSON to interact with APIs or store data locally. In this article, we will explore how to accomplish this using the `hydrated_bloc` package in Flutter.

## What is hydrated_bloc?

`hydrated_bloc` is a Flutter package that extends the default `bloc` package by providing an additional layer of persistence. It allows you to automatically persist and restore the state of your blocs even if the app restarts.

## Serializing JSON

Serializing JSON involves converting an object or a data structure into a JSON string. In Flutter, you can use the `json` package to accomplish this. Here is an example of serializing a custom class object:

```dart
import 'dart:convert';

class Person {
  String name;
  int age;

  Person(this.name, this.age);

  Map<String, dynamic> toJson() {
    return {
      'name': name,
      'age': age,
    };
  }

  factory Person.fromJson(Map<String, dynamic> json) {
    return Person(
      json['name'],
      json['age'],
    );
  }
}

void main() {
  Person person = Person('John Doe', 25);

  String jsonPerson = jsonEncode(person.toJson());

  print(jsonPerson);
}
```

In the above code, the `toJson()` method converts the `Person` object to a `Map` and then uses `jsonEncode` to convert the `Map` to a JSON string.

## Deserializing JSON

Deserializing JSON involves converting a JSON string into an object or data structure. In Flutter, you can use the `json` package to accomplish this as well. Here is an example of deserializing a JSON string into a custom class object:

```dart
import 'dart:convert';

class Person {
  String name;
  int age;

  // ...

  Map<String, dynamic> toJson() {
    // ...
  }

  factory Person.fromJson(Map<String, dynamic> json) {
    return Person(
      json['name'],
      json['age'],
    );
  }
}

void main() {
  String jsonPerson = '{"name": "John Doe", "age": 25}';

  Map<String, dynamic> personMap = jsonDecode(jsonPerson);

  Person person = Person.fromJson(personMap);

  print(person.name);
  print(person.age);
}
```

In the above code, the `fromJson()` method in the `Person` class takes a `Map` representing the JSON data and returns a `Person` object.

## Using hydrated_bloc

Now that we know how to serialize and deserialize JSON in Flutter, we can integrate it with `hydrated_bloc`. `hydrated_bloc` provides a mechanism to save and restore the state of your blocs, including JSON data.

To persist JSON data with `hydrated_bloc`, you need to override the `toJson()` and `fromJson()` methods in your bloc state class. Here's an example:

```dart
import 'package:hydrated_bloc/hydrated_bloc.dart';

class MyBlocState extends HydratedBloc {
  final String name;
  final int age;

  MyBlocState(this.name, this.age);

  @override
  Map<String, dynamic>? toJson() {
    return {
      'name': name,
      'age': age,
    };
  }

  @override
  MyBlocState? fromJson(Map<String, dynamic> json) {
    return MyBlocState(
      json['name'],
      json['age'],
    );
  }

  @override
  List<Object?> get props => [name, age];
}
```

In the above code, we override the `toJson()` and `fromJson()` methods to serialize and deserialize the `MyBlocState` class to/from JSON, respectively.

By leveraging the `toJson()` and `fromJson()` methods, you can easily store and retrieve your bloc state as JSON, ensuring persistence even when the app restarts.

## Conclusion

Serializing and deserializing JSON is a common task when working with APIs and data storage in Flutter. By combining `hydrated_bloc` with the `json` package, you can easily persist and restore your bloc state to and from JSON.

With `hydrated_bloc`, your Flutter app's state remains intact across app restarts, providing a seamless experience to the user.

#Flutter #JSON