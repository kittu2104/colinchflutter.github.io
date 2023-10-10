---
layout: post
title: "Flutter sqflite package for persistent state management"
description: " "
date: 2023-10-10
tags: [sqflite]
comments: true
share: true
---

![Flutter](https://www.gstatic.com/devrel-devsite/prod/v4f1ede05742e6a7798f9892675ca7642d670c74c79c0b92b3f104b7f8dd9c45d/flutter/images/lockup/logo/logomark.png)

Managing persistent state in Flutter applications can be a challenging task. Luckily, Flutter provides a variety of packages that make it easier to handle persistence, one of which is **sqflite**. In this blog post, we will explore how to use the sqflite package for persistent state management in Flutter.

## Table of Contents
- [Introduction to sqflite](#introduction-to-sqflite)
- [Setting up sqflite in your Flutter project](#setting-up-sqflite-in-your-flutter-project)
- [Creating a database and tables](#creating-a-database-and-tables)
- [Performing CRUD operations](#performing-crud-operations)
- [Querying and updating data](#querying-and-updating-data)
- [Conclusion](#conclusion)

## Introduction to sqflite
Sqflite is a Flutter package that provides a simple and efficient way to interact with SQLite databases. It allows you to store and retrieve data in a structured manner, making it ideal for persistent state management in Flutter applications.

## Setting up sqflite in your Flutter project
To get started with sqflite, you need to add it as a dependency in your Flutter project. Open your project's `pubspec.yaml` file and add the following line under the `dependencies` section:

```dart
dependencies:
  sqflite: ^2.0.0+3
```

After adding the dependency, run `flutter pub get` in your terminal to download and install the package.

## Creating a database and tables
Before you can start storing data, you need to create a database and define tables to store your data. Sqflite provides a simple API to handle these tasks.

To create a database, you can use the following code:

```dart
import 'package:sqflite/sqflite.dart';

void createDatabase() async {
  String path = await getDatabasesPath();
  String databasePath = join(path, 'my_database.db');

  Database database = await openDatabase(databasePath, version: 1,
      onCreate: (Database db, int version) {
    db.execute('CREATE TABLE users (id INTEGER PRIMARY KEY, name TEXT)');
  });
}
```

In this example, we use the `getDatabasesPath` method to get the path where the database will be stored. We then use the `openDatabase` method to create a new database with the specified path and version. In the `onCreate` callback, we can create our tables using SQL statements.

## Performing CRUD operations
Once you have created your database and tables, you can perform CRUD (Create, Read, Update, Delete) operations on them. Sqflite provides methods to handle these operations easily.

To insert data into a table, you can use the `insert` method:

```dart
void insertUser(String name) async {
  Database database = await openDatabase(databasePath);
  
  database.insert('users', {'name': name});
}
```

To retrieve data from a table, you can use the `query` method:

```dart
void getUsers() async {
  Database database = await openDatabase(databasePath);
  
  List<Map<String, dynamic>> users = await database.query('users');
}
```

To update data in a table, you can use the `update` method:

```dart
void updateUser(int id, String name) async {
  Database database = await openDatabase(databasePath);
  
  database.update('users', {'name': name}, where: 'id = ?', whereArgs: [id]);
}
```

To delete data from a table, you can use the `delete` method:

```dart
void deleteUser(int id) async {
  Database database = await openDatabase(databasePath);
  
  database.delete('users', where: 'id = ?', whereArgs: [id]);
}
```

## Querying and updating data
Sqflite provides powerful querying capabilities to filter and sort data. You can use the `query` method with various parameters to customize your queries.

For example, to fetch users with a specific name, you can use the following code:

```dart
void getUsersWithName(String name) async {
  Database database = await openDatabase(databasePath);
  
  List<Map<String, dynamic>> users = await database.query('users',
      where: 'name = ?', whereArgs: [name]);
}
```

To update multiple rows at once, you can use the `update` method with the `where` parameter:

```dart
void updateUsersWithName(String oldName, String newName) async {
  Database database = await openDatabase(databasePath);
  
  database.update('users', {'name': newName},
      where: 'name = ?', whereArgs: [oldName]);
}
```

## Conclusion
Sqflite offers a convenient way to manage persistent state in Flutter applications by providing an easy-to-use interface to SQLite databases. In this blog post, we covered the basics of setting up sqflite, creating databases and tables, performing CRUD operations, and querying and updating data.  With sqflite, you can efficiently handle persistent state management in your Flutter projects.

Give the sqflite package a try on your next Flutter project and see how it simplifies your persistent state management.

**#flutter #sqflite**