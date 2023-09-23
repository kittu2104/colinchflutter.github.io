---
layout: post
title: "Database handling extensions for Flutter"
description: " "
date: 2023-09-23
tags: [flutter, database]
comments: true
share: true
---

If you're working on a Flutter project that requires data persistence and querying capabilities, you'll likely need to integrate a database into your application. Fortunately, there are several database handling extensions available that can greatly simplify this task. In this blog post, we'll take a look at two popular options: `sqflite` and `moor`.

## 1. sqflite

`sqflite` is a robust and widely-used database handling extension for Flutter that allows you to interact with SQLite databases. It provides a simple and efficient API for performing CRUD (Create, Read, Update, Delete) operations, as well as advanced features like transactions and batch operations. Here's an example of how you can use `sqflite` to create a database and perform a simple query:

```dart
import 'package:sqflite/sqflite.dart';
import 'package:path/path.dart';

void main() async {
  final database = openDatabase(
    join(await getDatabasesPath(), 'my_database.db'),
    onCreate: (db, version) {
      return db.execute(
        'CREATE TABLE my_table(id INTEGER PRIMARY KEY, name TEXT)',
      );
    },
    version: 1,
  );

  await database.then((Database db) async {
    final List<Map<String, dynamic>> rows = await db.query('my_table');
    rows.forEach((row) {
      print(row);
    });
  });
}
```

By using `sqflite`, you can easily create tables, insert data, query records, update existing entries, and delete data within your Flutter app.

## 2. moor

`moor` is another popular database handling extension for Flutter that provides a type-safe and reactive programming model for database interactions. It allows you to define your database schema using Dart code, enabling compile-time checks for queries and migrations. Here's a simple example of using `moor` to create a database and perform a query:

```dart
import 'package:moor_flutter/moor_flutter.dart';

class MyTable extends Table {
  IntColumn get id => integer().autoIncrement()();
  TextColumn get name => text()();
}

@UseMoor(tables: [MyTable])
class MyDatabase extends _$MyDatabase {
  MyDatabase()
      : super(FlutterQueryExecutor.inDatabaseFolder(
            path: 'my_database.sqlite', logStatements: true));

  @override
  int get schemaVersion => 1;

  Future<List<MyTableData>> getAllRecords() => select(myTable).get();
}

void main() async {
  final database = MyDatabase();
  final records = await database.getAllRecords();

  records.forEach((record) {
    print(record.name);
  });
}
```

With `moor`, you can define your database schema using Dart classes and leverage powerful DSL (Domain Specific Language) queries. It also provides support for joins, complex queries, and migrations.

## Conclusion

When working on a Flutter project that requires database handling, extensions like `sqflite` and `moor` can greatly simplify your development process. Whether you prefer a lightweight SQLite-based approach or a type-safe, reactive model, these extensions offer powerful and flexible solutions for integrating databases into your Flutter applications.

#flutter #database