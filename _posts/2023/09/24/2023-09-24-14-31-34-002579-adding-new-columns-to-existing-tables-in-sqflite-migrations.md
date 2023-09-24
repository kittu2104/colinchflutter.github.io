---
layout: post
title: "Adding new columns to existing tables in sqflite migrations"
description: " "
date: 2023-09-24
tags: [Flutter, DatabaseMigrations]
comments: true
share: true
---

Migrations are an essential part of database management, allowing you to modify the structure of your database schema without losing any data. In this article, we'll explore how to add new columns to existing tables using the `sqflite` package in Flutter.

## Prerequisites
Before we start, make sure you have the `sqflite` package added as a dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  sqflite: ^x.x.x
```

Make sure to replace `x.x.x` with the latest version of `sqflite` available.

## Updating the Database
To add a new column to an existing table, you need to follow these steps:

### Step 1: Create a Migration File
Create a new migration file by extending the `Migration` class provided by `sqflite`. Let's say we want to add a `last_modified` column of type `DateTime` to an existing table called `notes`. Here's an example migration file:

```dart
import 'package:sqflite/sqflite.dart';
import 'package:path/path.dart';

class AddLastModifiedColumn extends Migration {
  @override
  Future<void> up(Database db, int version) async {
    await db.execute('ALTER TABLE notes ADD COLUMN last_modified TEXT');
  }

  @override
  Future<void> down(Database db, int version) async {
    // Revert the changes if needed
    await db.execute('ALTER TABLE notes DROP COLUMN last_modified');
  }
}
```

### Step 2: Run the Migration
To run the migration and apply the changes to your database, you need to call the `database.execute` method and pass an instance of your migration class.

```dart
Future<void> updateDatabase(Database database, int oldVersion, int newVersion) async {
  for (var i = oldVersion + 1; i <= newVersion; i++) {
    switch (i) {
      // Add new migration cases as you update your schema
      case 2:
        await database.execute(AddLastModifiedColumn().upSql);
        break;
    }
  }
}
```

In the example above, the migration is applied only when upgrading from version 1 to version 2.

### Step 3: Update Database Version
Before running the migration, make sure to update the database version in your `openDatabase` function:

```dart
final database = await openDatabase(
  join(await getDatabasesPath(), 'my_database.db'),
  version: 2,
  onCreate: (db, version) {
    // Handle initial database creation
  },
  onUpgrade: (db, oldVersion, newVersion) async {
    await updateDatabase(db, oldVersion, newVersion);
  },
);
```

Ensure that the `version` parameter matches the latest version you've added in the migration code.

### Step 4: Testing
To ensure that the migration runs successfully, you can either run your app and let the migration happen automatically, or you can manually trigger the migration process by uninstalling and reinstalling the app.

Make sure to test the migration thoroughly to validate that the new column is added successfully and behaves as expected.

## Conclusion
Migrating your database schema is a crucial aspect of database management. `sqflite` provides a simple and efficient way to modify existing tables by adding new columns. By following the steps outlined in this article, you'll be able to seamlessly update your database schema without losing any data.

#Flutter #DatabaseMigrations