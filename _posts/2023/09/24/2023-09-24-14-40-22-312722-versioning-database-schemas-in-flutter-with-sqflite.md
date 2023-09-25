---
layout: post
title: "Versioning database schemas in Flutter with sqflite"
description: " "
date: 2023-09-24
tags: [sqflite]
comments: true
share: true
---

Database schemas are an essential part of any mobile application that requires persistent storage. As your application evolves and new features are added, you may find yourself needing to make changes to the database schema. This can include adding new tables, modifying existing tables, or even altering data types.

To ensure the smooth transition between schema changes, it is crucial to handle database versioning effectively. In this blog post, we will explore how to version your database schemas in Flutter using the popular sqflite package.

## 1. Understanding Database Versioning

Database versioning is a mechanism that allows your application to manage changes in the database schema over time. Each time you make a significant change to the schema, you increment the database version number. This ensures that your app can detect the changes and apply the necessary modifications during runtime.

## 2. Implementing Versioning with sqflite

To implement versioning in your Flutter app using sqflite, follow these steps:

### Step 1: Define a `DatabaseOpenHelper` class

Create a class that extends the `DatabaseOpenHelper` class from the sqflite package. This class will be responsible for opening, creating, and upgrading the database.

```dart
import 'package:sqflite/sqflite.dart';

class DatabaseHelper extends DatabaseOpenHelper {
  static const databaseName = 'my_database.db';
  static const databaseVersion = 1;

  @override
  void onCreate(Database db, int version) {
    // Create initial schema
    db.execute('''
      CREATE TABLE users (
        id INTEGER PRIMARY KEY,
        name TEXT,
        age INTEGER
      )
    ''');
  }

  @override
  void onUpgrade(Database db, int oldVersion, int newVersion) {
    // Handle schema modifications based on old and new version numbers
    if (oldVersion < 2) {
      db.execute('ALTER TABLE users ADD COLUMN email TEXT');
    }
    if (oldVersion < 3) {
      // Handle other schema modifications for version 3 and so on
    }
  }
}
```

### Step 2: Open or Create the Database

To initialize the database, create an instance of the `DatabaseHelper` class and call the `open()` method. If the database does not already exist, it will be created at this step.

```dart
Database database = await DatabaseHelper().open(databaseName: DatabaseHelper.databaseName);
```

### Step 3: Handle Database Upgrades

To handle database upgrades, modify the `databaseVersion` constant in the `DatabaseHelper` class. Whenever you make changes to the schema, increment this number. When the app opens, the `onUpgrade()` method will be called, allowing you to handle database modifications based on the old and new version numbers.

```dart
class DatabaseHelper extends DatabaseOpenHelper {
  static const databaseName = 'my_database.db';
  static const databaseVersion = 2;

  // ...
}
```

## 3. Conclusion

Versioning your database schemas in Flutter apps using sqflite is a crucial aspect of maintaining data integrity when making schema modifications. By implementing the steps outlined in this blog post, you can efficiently handle database changes and ensure a smooth experience for your users.

#flutter #sqflite