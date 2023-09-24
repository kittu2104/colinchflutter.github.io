---
layout: post
title: "Adding indexes to tables in Flutter database migrations"
description: " "
date: 2023-09-24
tags: [Flutter, DatabaseMigration]
comments: true
share: true
---

When working with a Flutter app that uses a local database, it's important to optimize the performance of database queries. One way to achieve this is by adding indexes to tables. Indexes improve the speed of searching and sorting data in a table.

In this blog post, we will explore how to add indexes to tables in Flutter database migrations. We will specifically focus on using the `sqflite` package, which is a popular SQLite plugin for Flutter.

## Creating a Migration File

To add an index to a table in Flutter, we need to create a migration file. A migration file is responsible for updating the database schema, including any changes to tables, columns, or indexes.

First, let's create a new migration file. Assuming we have a table called `users` that we want to add an index to, we can create a migration file named `2_add_users_index.dart`. The number in the file name is used to keep track of the order in which migrations are applied.

## Writing a Migration

Inside the migration file, we need to extend the `Migration` class provided by the `sqflite` package. We will implement the `up` method, which is called when the migration is applied.

```dart
import 'package:sqflite/sqlite_api.dart';
import 'package:sqflite_common/sqlite_api.dart' as sqlite;

class AddUsersIndex extends Migration {
  @override
  Future<void> up(Database database, int version) async {
    await database.execute('CREATE INDEX users_name_index ON users(name)');
  }
}
```

In the `up` method, we use the `execute` method of the `Database` class to execute a SQL statement that creates an index on the `name` column of the `users` table. The index is named `users_name_index`.

Make sure to import the necessary packages for `Database` and the `Migration` class. Additionally, import both `sqlite_api.dart` and `sqlite_api.dart` to ensure compatibility with different platforms.

## Applying the Migration

To apply the migration, we need to include it in the list of migrations when opening the database.

```dart
import 'package:sqflite/sqflite.dart';

Future<void> main() async {
  final database = await openDatabase(
    'path_to_database',
    version: 2,
    onCreate: (db, version) {
      // Initial table creation
    },
    onUpgrade: (db, oldVersion, newVersion) {
      // Handle migrations
      if (newVersion == 2) {
        final migration = AddUsersIndex();
        migration.up(db, newVersion);
      }
      // Add more migrations if required
    },
  );

  // Use the database

  await database.close();
}
```

In the `onUpgrade` callback, we check if the new version of the database matches the version in which we want to apply the migration (in this case, version 2). If it does, we create an instance of our `AddUsersIndex` migration class and call the `up` method.

Remember to replace `'path_to_database'` with the actual path to your database file.

## Conclusion

By adding indexes to tables in your Flutter app's database migrations, you can significantly improve the performance of data retrieval and sorting operations. The implementation is straightforward, thanks to the `sqflite` package's powerful capabilities for working with SQLite databases.

#Flutter #DatabaseMigration