---
layout: post
title: "Setting up a SQLite database in Flutter"
description: " "
date: 2023-09-24
tags: [SQLite]
comments: true
share: true
---

Flutter is a popular cross-platform framework for building beautiful and high-performance mobile applications. When developing mobile apps, it's often necessary to persist data locally on the device. SQLite is a lightweight and widely-used database engine that provides a simple and efficient way to store and retrieve data in a structured format.

In this blog post, we will explore how to set up a SQLite database in a Flutter application. We will cover the steps required to initialize the database, create tables and perform basic CRUD operations.

## Step 1: Adding Dependencies
First, we need to add the necessary dependencies to our `pubspec.yaml` file. Open the file and add the following lines:

```yaml
dependencies:
  sqflite: ^x.x.x
  path: ^x.x.x
```

Replace `x.x.x` with the latest version of `sqflite` and `path` packages.

## Step 2: Initializing the Database
To interact with the SQLite database, we need to create a database helper class. Create a new file called `database_helper.dart` and add the following code:

```dart
import 'package:sqflite/sqflite.dart';
import 'package:path/path.dart';

class DatabaseHelper {
  static Database _database;

  Future<Database> get database async {
    if (_database != null) {
      return _database;
    }

    _database = await _initDatabase();
    return _database;
  }

  Future<Database> _initDatabase() async {
    String databasePath = await getDatabasesPath();
    String path = join(databasePath, 'my_database.db');

    return await openDatabase(
      path,
      version: 1,
      onCreate: _createTables,
    );
  }

  Future<void> _createTables(Database db, int version) async {
    await db.execute('''
      CREATE TABLE IF NOT EXISTS user (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        name TEXT,
        age INTEGER
      )
    ''');
  }
}
```

The above code sets up the database and creates a `user` table with three columns: `id`, `name`, and `age`. 

## Step 3: CRUD Operations
Now that we have set up the database, let's explore how to perform CRUD (Create, Read, Update, Delete) operations on our database.

###  Creating a User
To insert a new user into the `user` table, we can define a method like this:

```dart
Future<int> createUser(User user) async {
  final db = await database;
  return await db.insert('user', user.toMap());
}
```

### Reading Users
To fetch all the users from the `user` table, we can implement a method like this:

```dart
Future<List<User>> getUsers() async {
  final db = await database;
  final List<Map<String, dynamic>> maps = await db.query('user');
  return List.generate(maps.length, (i) {
    return User(
      id: maps[i]['id'],
      name: maps[i]['name'],
      age: maps[i]['age'],
    );
  });
}
```

### Updating a User
To update an existing user in the `user` table, we can define a method like this:

```dart
Future<void> updateUser(User user) async {
  final db = await database;
  await db.update(
    'user',
    user.toMap(),
    where: 'id = ?',
    whereArgs: [user.id],
  );
}
```

### Deleting a User
To delete a user from the `user` table, we can implement a method like this:

```dart
Future<void> deleteUser(int userId) async {
  final db = await database;
  await db.delete(
    'user',
    where: 'id = ?',
    whereArgs: [userId],
  );
}
```

## Conclusion
In this blog post, we have learned how to set up a SQLite database in a Flutter application. We covered the steps to initialize the database, create tables, and perform basic CRUD operations. By leveraging the power of SQLite, we can now easily persist and manipulate data in our Flutter apps.

#Flutter #SQLite