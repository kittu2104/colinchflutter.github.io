---
layout: post
title: "Executing migrations using the sqflite package in Flutter"
description: " "
date: 2023-09-24
tags: [flutter, sqflite]
comments: true
share: true
---

Migrations are an essential part of database management that allow developers to make changes to the structure of the database schema without losing existing data. In Flutter, the **sqflite** package provides a convenient way to handle migrations when working with a SQLite database.

## Adding sqflite to Your Project

First, you need to add the **sqflite** package to your Flutter project. Open the `pubspec.yaml` file and add the following line under the `dependencies` section:

```yaml
dependencies:
  sqflite: ^2.0.0
```

Run `flutter pub get` to fetch the package and update your project.

## Configuring Migrations

To execute migrations with sqflite, you need to define a database helper class that extends the `DatabaseOpenHelper` class provided by sqflite. This class will handle creating and upgrading the database schema.

Create a new file called `database_helper.dart` and add the following code:

```dart
import 'package:sqflite/sqflite.dart';
import 'package:path/path.dart';

class DatabaseHelper {
  static final _databaseName = 'my_database.db';
  static final _databaseVersion = 1;

  static final migrationScripts = [
    '''
    CREATE TABLE IF NOT EXISTS my_table (
      id INTEGER PRIMARY KEY,
      name TEXT,
      age INTEGER
    );
    '''
  ];

  static Future<Database> open() async {
    final databasesPath = await getDatabasesPath();
    final path = join(databasesPath, _databaseName);

    return openDatabase(
      path,
      version: _databaseVersion,
      onCreate: (db, version) async {
        for (final script in migrationScripts) {
          await db.execute(script);
        }
      },
      onUpgrade: (db, oldVersion, newVersion) {
        // Perform migrations if needed
      },
    );
  }
}
```

In this code snippet, we define the `_databaseName` and `_databaseVersion` variables to specify the name and version of the database. We also define a `migrationScripts` list, which contains the SQL scripts for creating tables or performing any other necessary migrations. In our example, we create a new table called `my_table`.

The `open` method is responsible for opening the database and executing migrations. The `onCreate` callback is called when the database is created for the first time, and it executes all the migration scripts. The `onUpgrade` callback allows you to handle any upgrades or changes to the schema.

## Using the Database Helper

To use the `DatabaseHelper` class to execute migrations and interact with the database, you can call the `open` method to get an instance of the database. Here's an example:

```dart
void main() async {
  final database = await DatabaseHelper.open();
  // Use the database instance
}
```

With the database instance, you can perform various operations like inserting, updating, or querying data.

## Conclusion

Migrations are crucial for managing the schema of a database. The **sqflite** package in Flutter provides a straightforward way to handle migrations. By following the steps outlined in this article, you can execute migrations effortlessly and make changes to your SQLite database schema without losing any existing data.

#flutter #sqflite