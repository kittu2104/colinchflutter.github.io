---
layout: post
title: "Using local databases with MaterialApp."
description: " "
date: 2023-10-23
tags: [databases]
comments: true
share: true
---

When developing mobile applications, it is often necessary to store data locally on the device. This allows for offline access and better performance. One way to achieve this is by using a local database in your application.

In this tutorial, we will explore how to use a local database with the MaterialApp framework to store and retrieve data in your mobile app.

## Table of Contents
- [Introduction](#introduction)
- [Setting Up the Database](#setting-up-the-database)
- [Creating the Database Helper](#creating-the-database-helper)
- [Using the Database in MaterialApp](#using-the-database-in-materialapp)
- [Conclusion](#conclusion)

## Introduction

A local database, such as SQLite, is a lightweight and serverless database that allows you to store structured data on the device. By using a local database, you can easily perform operations like CRUD (Create, Read, Update, Delete) on the data stored in your application.

The MaterialApp framework is a popular choice for building mobile applications using Google's Flutter SDK. It provides a set of pre-designed UI components and state management tools.

## Setting Up the Database

To use a local database in your MaterialApp app, you first need to add the necessary dependencies to your `pubspec.yaml` file. Open the file and add the following lines:

```yaml
dependencies:
  sqflite: ^2.0.0
  path_provider: ^2.0.2
```

Save the file and run `flutter pub get` to fetch the new dependencies.

## Creating the Database Helper

Next, we need to create a database helper class that will handle all the operations related to the database. In this example, we will create a simple class called `DatabaseHelper`. Inside this class, we will define methods to create the database, insert data, retrieve data, update data, and delete data.

```dart
import 'dart:io';
import 'package:path/path.dart';
import 'package:sqflite/sqflite.dart';
import 'package:path_provider/path_provider.dart';

class DatabaseHelper {
  static final _databaseName = "my_database.db";
  static final _databaseVersion = 1;

  static Database? _database;

  Future<Database?> get database async {
    if (_database != null) return _database;
    _database = await _initDatabase();
    return _database;
  }

  _initDatabase() async {
    Directory documentsDirectory = await getApplicationDocumentsDirectory();
    String path = join(documentsDirectory.path, _databaseName);
    return await openDatabase(path, version: _databaseVersion, onCreate: _onCreate);
  }

  Future<void> _onCreate(Database db, int version) async {
    await db.execute(
        "CREATE TABLE my_table (id INTEGER PRIMARY KEY AUTOINCREMENT, name TEXT, email TEXT)");
  }

  // Add methods for database operations
  // ... Insert, retrieve, update, and delete data
}
```
In the above code, we create a singleton for the database object, which ensures that only one instance is created throughout the app's lifecycle. The `get database` method returns this singleton instance. Inside the `_initDatabase` method, we create the database if it doesn't exist and specify the database schema if necessary.

## Using the Database in MaterialApp

Now that we have set up the database helper class, we can use it in our MaterialApp app. Let's say we want to display a list of users from the database. We can create a separate class called `UserListPage` that extends StatelessWidget and retrieves the user data from the local database.

```dart
import 'package:flutter/material.dart';

class UserListPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('User List'),
      ),
      body: Center(
        child: FutureBuilder<List<User>>(
          future: DatabaseHelper().getAllUsers(),
          builder: (context, snapshot) {
            if (snapshot.hasData) {
              return ListView.builder(
                itemCount: snapshot.data!.length,
                itemBuilder: (BuildContext context, int index) {
                  User user = snapshot.data![index];
                  return ListTile(
                    title: Text(user.name),
                    subtitle: Text(user.email),
                  );
                },
              );
            } else {
              return CircularProgressIndicator();
            }
          },
        ),
      ),
    );
  }
}
```

In the above code, we create a `UserListPage` that uses the `FutureBuilder` widget to asynchronously retrieve the list of users from the database. If the data is available, we display it in a `ListView.builder` widget. Otherwise, we display a loading indicator.

You can navigate to this page from your MaterialApp app by using the `Navigator.push` method. For example:

```dart
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => UserListPage()),
);
```

## Conclusion

In this tutorial, we learned how to use a local database with the MaterialApp framework to store and retrieve data in a mobile app. We created a database helper class to handle database operations and displayed a list of users from the database using the FutureBuilder widget.

Using a local database can greatly improve the performance and offline capabilities of your mobile application. Feel free to explore more database operations and customize the user interface based on your application's requirements.

# References
- [Flutter Documentation](https://flutter.dev/docs)
- [sqflite package](https://pub.dev/packages/sqflite)
- [path_provider package](https://pub.dev/packages/path_provider)

#flutter #databases