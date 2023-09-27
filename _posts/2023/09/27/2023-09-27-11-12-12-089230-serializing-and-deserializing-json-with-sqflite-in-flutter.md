---
layout: post
title: "Serializing and deserializing JSON with sqflite in Flutter"
description: " "
date: 2023-09-27
tags: [sqflite, JSON]
comments: true
share: true
---

If you are building a Flutter application that needs to persist data locally, you may consider using the `sqflite` package to work with a SQLite database. When dealing with JSON data, you might need to **serialize** (convert an object to JSON) and **deserialize** (convert JSON back to an object) the data.

In this blog post, we will explore how to serialize and deserialize JSON data with `sqflite` in Flutter.

## 1. Serializing JSON

To serialize an object to JSON, you will need to convert the object properties into a JSON format. The `dart:convert` library provides a helper class called `json` that makes it easy to work with JSON data.

Consider the following example:

```dart
import 'dart:convert';

class Person {
  final String name;
  final int age;

  Person(this.name, this.age);

  Map<String, dynamic> toJson() {
    return {
      'name': name,
      'age': age,
    };
  }
}

void main() {
  Person person = Person('John Doe', 30);
  String json = jsonEncode(person.toJson());
  print(json); // Output: {"name":"John Doe","age":30}
}
```

In the above code, the `Person` class has a `toJson` method that returns a `Map<String, dynamic>` representing the object's properties. The `jsonEncode` function serializes the `Map` object to a JSON string.

## 2. Deserializing JSON

Deserializing JSON means converting a JSON string back into an object of a specific class. You can use the `jsonDecode` function from the `dart:convert` library to achieve this.

Continuing from the previous example, let's see how to deserialize the JSON string back into a `Person` object:

```dart
void main() {
  String json = '{"name":"John Doe","age":30}';
  Map<String, dynamic> jsonData = jsonDecode(json);
  Person person = Person(jsonData['name'], jsonData['age']);

  print(person.name); // Output: John Doe
  print(person.age); // Output: 30
}
```

Here, the `jsonDecode` function converts the JSON string into a `Map<String, dynamic>`. We can then use the values from the map to create a new `Person` object.

## 3. Storing Serialized JSON into sqflite

Now that you know how to serialize and deserialize JSON objects, let's go one step further and explore how to store JSON data into `sqflite` database tables.

First, create a database table schema that can store the JSON data. For example:

```dart
await db.execute('''
  CREATE TABLE IF NOT EXISTS person (
    id INTEGER PRIMARY KEY,
    json_data TEXT
  )
''');
```

Once the table is set up, use the serialization and deserialization techniques we discussed earlier to store and retrieve JSON data:

```dart
void insertPerson(Person person) async {
  final db = await database;
  await db.insert('person', {'json_data': jsonEncode(person.toJson())});
}

Future<List<Person>> getAllPersons() async {
  final db = await database;
  final List<Map<String, dynamic>> jsonList =
      await db.query('person');

  return jsonList.map((json) => Person.fromJson(jsonDecode(json['json_data']))).toList();
}
```

In the `insertPerson` function, we serialize the `Person` object and insert it into the `person` table as a JSON string. In the `getAllPersons` function, we retrieve the JSON data from the database and deserialize it back into `Person` objects.

By following these steps, you can effectively use `sqflite` to store and retrieve JSON data in your Flutter application.

## Conclusion

In this blog post, we explored how to serialize and deserialize JSON data with `sqflite` in Flutter. We learned how to convert objects to JSON using the `dart:convert` library, and how to store and retrieve JSON data in a `sqflite` database.

Using these techniques, you can seamlessly work with JSON data in your Flutter application, making it easier to persist and manipulate complex data structures.

#flutter #sqflite #JSON #serialization #deserialization