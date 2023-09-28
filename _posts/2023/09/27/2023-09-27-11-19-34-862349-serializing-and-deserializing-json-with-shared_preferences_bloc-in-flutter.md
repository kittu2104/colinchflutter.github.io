---
layout: post
title: "Serializing and deserializing JSON with shared_preferences_bloc in Flutter"
description: " "
date: 2023-09-27
tags: []
comments: true
share: true
---

In Flutter, `shared_preferences_bloc` is a package that provides an easy way to save and retrieve data using key-value pair storage. JSON (JavaScript Object Notation) is a popular data format used for transmitting data between a server and a client. In this article, we'll explore how to serialize and deserialize JSON data using `shared_preferences_bloc` in Flutter.

## What is Serializing?

Serializing refers to the process of converting an object into a format that can be stored or transmitted. In the context of JSON, serializing means converting an object into a JSON string.

## What is Deserializing?

Deserializing is the opposite of serializing. It is the process of converting a serialized object (such as a JSON string) back into an object.

## Using shared_preferences_bloc for Serializing and Deserializing JSON

To use `shared_preferences_bloc` for serializing and deserializing JSON in Flutter, follow these steps:

### 1. Import the required packages

First, add the `shared_preferences_bloc` package in your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  shared_preferences_bloc: ^0.2.1
```

Then, import the necessary Dart packages in your Dart file:

```dart
import 'dart:convert';

import 'package:shared_preferences/shared_preferences.dart';
import 'package:shared_preferences_bloc/shared_preferences_bloc.dart';
```

### 2. Serializing JSON Data

To serialize an object to JSON and save it in the shared preferences, follow these steps:

#### a. Create a model class

Create a model class to represent the data you want to serialize. Make sure the class extends `JsonSerializable`.

```dart
class Person extends JsonSerializable {
  final String name;
  final int age;

  Person(this.name, this.age);

  Map<String, dynamic> toJson() => {
        "name": name,
        "age": age,
      };

  static Person fromJson(Map<String, dynamic> json) =>
      Person(json["name"], json["age"]);
}
```

#### b. Serialize the object and save it

```dart
void savePerson(Person person) async {
  final prefs = await SharedPreferences.getInstance();
  prefs.setString('person', jsonEncode(person.toJson()));
}
```

### 3. Deserializing JSON Data

To deserialize the JSON data saved in shared preferences, follow these steps:

#### a. Retrieve the saved JSON string

```dart
String getSavedPersonJson() {
  final prefs = SharedPreferencesBloc();
  return prefs.getString('person') ?? '';
}
```

#### b. Deserialize the JSON string to an object

```dart
Person getSavedPerson() {
  final json = getSavedPersonJson();
  if (json.isNotEmpty) {
    final personMap = jsonDecode(json);
    return Person.fromJson(personMap);
  }
  return null;
}
```

## Conclusion

Serializing and deserializing JSON data with `shared_preferences_bloc` in Flutter is a convenient way to store and retrieve objects. By following the steps outlined in this article, you can easily serialize your objects to JSON and save them in shared preferences. Additionally, you can retrieve the JSON data and deserialize it back into an object when needed.