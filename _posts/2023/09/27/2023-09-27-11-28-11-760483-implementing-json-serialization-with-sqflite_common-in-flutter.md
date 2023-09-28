---
layout: post
title: "Implementing JSON serialization with sqflite_common in Flutter"
description: " "
date: 2023-09-27
tags: []
comments: true
share: true
---

In many Flutter applications, the need to store and retrieve data from a local database arises. One popular plugin for managing local databases is `sqflite`, which provides a simple and efficient way to interact with SQLite databases in Flutter.

However, when working with databases, it is often necessary to serialize and deserialize complex data types, such as JSON. In this blog post, we will explore how to implement JSON serialization with `sqflite_common` in Flutter.

## Step 1: Adding Dependencies

To get started, add the necessary dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  sqflite: ^2.0.0+3
  sqflite_common: ^2.0.2+2
  path: ^2.2.2
  json_annotation: ^4.0.0
  build_runner: ^2.1.4
```

After adding the dependencies, run `flutter pub get` to fetch them in your Flutter project.

## Step 2: Creating the Database Model

Next, create a model class that represents the data you want to store and retrieve from the database. Let's say we have a `User` class with the following properties:

```dart
import 'package:json_annotation/json_annotation.dart';

part 'user_model.g.dart';

@JsonSerializable()
class User {
  int id;
  String name;
  int age;

  User(this.id, this.name, this.age);

  factory User.fromJson(Map<String, dynamic> json) => _$UserFromJson(json);
  Map<String, dynamic> toJson() => _$UserToJson(this);
}
```

The `@JsonSerializable()` annotation is used to generate the necessary JSON serialization code.

## Step 3: Generating JSON Serialization Code

To generate the JSON serialization code for your model class, run the following command in your project's root directory:

```bash
flutter packages pub run build_runner build
```

This command will generate the serialization code in a new file called `user_model.g.dart`.

## Step 4: Creating the Database Helper

Now, let's create a database helper class that will handle the database operations. Here's an example:

```dart
import 'package:sqflite/sqflite.dart' as sqflite;
import 'package:path/path.dart' as path;

class DatabaseHelper {
  static const databaseName = 'app.db';
  static sqflite.Database? _database;

  static Future<sqflite.Database> get database async {
    return _database ??= await _initDatabase();
  }

  static Future<sqflite.Database> _initDatabase() async {
    final dbPath = await sqflite.getDatabasesPath();
    final pathToFile = path.join(dbPath, databaseName);

    return sqflite.openDatabase(
      pathToFile,
      onCreate: (db, version) {
        return db.execute('''
          CREATE TABLE users (
              id INTEGER PRIMARY KEY AUTOINCREMENT,
              name TEXT,
              age INTEGER
          )
        ''');
      },
      version: 1,
    );
  }

  static Future<int> insertUser(User user) async {
    final db = await database;

    return db.insert(
      'users',
      user.toJson(),
      conflictAlgorithm: sqflite.ConflictAlgorithm.replace,
    );
  }

  static Future<List<User>> getUsers() async {
    final db = await database;

    final queryResult = await db.query('users');

    return queryResult.map((json) => User.fromJson(json)).toList();
  }
}
```

In the database helper class, we define methods for inserting users into the database (`insertUser`) and retrieving users from the database (`getUsers`).

## Step 5: Using JSON Serialization with Sqflite

Now that we have set up the necessary classes, we can use JSON serialization when working with the database. For example, to insert a user into the database:

```dart
final user = User(1, 'John Doe', 25);
await DatabaseHelper.insertUser(user);
```

To retrieve all users from the database:

```dart
final users = await DatabaseHelper.getUsers();
```

With JSON serialization implemented, you can easily store and retrieve complex data types like JSON objects when working with `sqflite` in Flutter.

#flutter #flutterdevelopment