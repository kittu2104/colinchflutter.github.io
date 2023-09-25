---
layout: post
title: "Conditional migrations based on app version in sqflite"
description: " "
date: 2023-09-24
tags: [DatabaseMigrations]
comments: true
share: true
---

When working with databases in mobile applications, it's common to need to perform migrations to update the database schema as your app evolves. However, in some cases, you may want to apply migrations conditionally based on the app version to ensure a smooth transition for your users. In this blog post, we'll explore how to implement conditional migrations based on app version using the `sqflite` package in Flutter.

## Understanding Migrations

Before we dive into conditional migrations, let's quickly recap the concept of migrations. Migrations are a way to modify the database schema over time, typically adding or modifying tables, columns, or indices. With each app update, you can apply the necessary migrations to ensure that the database schema remains up-to-date.

## Setting Up the Database

To get started, make sure you have the `sqflite` package added as a dependency in your Flutter project. You can do this by adding the following line to your `pubspec.yaml` file:

```dart
dependencies:
  sqflite: ^2.0.0
```

Next, create a database helper class that will handle the database creation and migrations. Here's an example of how you can set up the class:

```dart
import 'package:sqflite/sqflite.dart';

class DatabaseHelper {
  static Database? _database;

  static Future<Database> get database async {
    if (_database != null) {
      return _database!;
    }

    _database = await _initializeDatabase();
    return _database!;
  }

  static Future<Database> _initializeDatabase() async {
    // Initialize database and apply migrations here
  }
}
```

## Applying Conditional Migrations

To apply conditional migrations based on the app version, you can use the `deleteDatabase` method from the `sqflite` package to drop the existing database and recreate it with the updated schema. Here's an example of how you can implement this in the `_initializeDatabase` method:

```dart
 static Future<Database> _initializeDatabase() async {
    final databasePath = await getDatabasesPath();
    final path = join(databasePath, 'my_database.db');

    // Delete existing database if it exists
    await deleteDatabase(path);

    // Recreate the database
    final database = await openDatabase(path, version: 1,
        onCreate: (Database db, int version) async {
      // Create initial tables here
    });

    // Perform conditional migrations based on app version
    final currentVersion = await getAppVersion();
    if (currentVersion < 2) {
      // Apply migration for version 2
      await database.execute('ALTER TABLE my_table ADD COLUMN new_column TEXT');
    }

    if (currentVersion < 3) {
      // Apply migration for version 3
      await database.execute('CREATE TABLE new_table (id INTEGER PRIMARY KEY, name TEXT)');
    }

    // Update the app version
    await saveAppVersion(3);

    return database;
  }
```

In the example above, we first delete the existing database if it exists. We then recreate the database using the `openDatabase` method. Within the `onCreate` callback, you can create the initial tables required by your app.

After that, we retrieve the current app version using a separate method `getAppVersion()`. We can then perform conditional migrations based on the current version. In this example, we're applying two migrations for versions 2 and 3, respectively. Once the migrations are complete, we update the app version using the `saveAppVersion()` method.

## Conclusion

Implementing conditional migrations based on app version is crucial for ensuring a seamless database schema update process in your mobile applications. By using the `sqflite` package and following the steps outlined in this blog post, you'll be able to handle migrations effectively and keep your user's data intact across app updates.

Remember to always test your migrations thoroughly before releasing any updates to ensure a smooth user experience. Happy coding!

**#Flutter #DatabaseMigrations**