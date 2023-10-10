---
layout: post
title: "Flutter SQL package for local state management"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

In Flutter, managing local state is essential for building reactive and performant applications. One popular approach for local state management is using a database to store and retrieve information. In this blog post, we will explore the **flutter_sql** package, a powerful tool for integrating SQL databases into Flutter applications.

## Table of Contents
- [Introduction](#introduction)
- [Installation](#installation)
- [Usage](#usage)
- [Example](#example)
- [Conclusion](#conclusion)
- [Resources](#resources)

## Introduction

The **flutter_sql** package is a lightweight SQLite database plugin specifically designed for Flutter. It allows you to easily create, read, update, and delete records in a local SQLite database. With its intuitive API, you can efficiently perform database operations, making it an excellent choice for local state management in Flutter applications.

## Installation

To install the **flutter_sql** package, add it to your project's dependencies in the `pubspec.yaml` file:

```yaml
dependencies:
  flutter_sql: ^1.0.0
```

Then, run `flutter pub get` to fetch the package.

## Usage

Before using **flutter_sql**, make sure to import the necessary libraries:

```dart
import 'package:flutter_sql/flutter_sql.dart';
```

To create a database and perform database operations, follow these steps:

1. Create a database instance:

   ```dart
   final database = await SqliteClient.create("mydatabase.db");
   ```

2. Define a schema for your database:

   ```dart
   final schema = Schema(
     version: 1,
     tables: [
       Table(
         name: "books",
         columns: [
           Column(name: "id", type: ColumnType.integer, primaryKey: true),
           Column(name: "title", type: ColumnType.text),
           Column(name: "author", type: ColumnType.text),
         ],
       ),
     ],
   );
   await database.setSchema(schema);
   ```

3. Perform database operations:

   - Insert a record:

     ```dart
     final book = {
       "id": 1,
       "title": "Flutter in Action",
       "author": "Eric Windmill",
     };
     await database.insert("books", book);
     ```

   - Query records:

     ```dart
     final result = await database.query("SELECT * FROM books");
     final books = result.toList();
     ```

   - Update a record:

     ```dart
     final updatedBook = {
       "id": 1,
       "title": "Flutter in Action (Updated)",
       "author": "Eric Windmill (Updated)",
     };
     await database.update("books", updatedBook);
     ```

   - Delete a record:

     ```dart
     await database.delete("books", where: "id = ?", whereArgs: [1]);
     ```

## Example

Let's take a look at an example that demonstrates the use of **flutter_sql** for local state management in a Flutter application. Suppose we have an application that allows users to create and manage a list of books.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_sql/flutter_sql.dart';

class Book {
  final int id;
  final String title;
  final String author;

  Book({required this.id, required this.title, required this.author});
}

class BookListScreen extends StatefulWidget {
  @override
  _BookListScreenState createState() => _BookListScreenState();
}

class _BookListScreenState extends State<BookListScreen> {
  final database = SqliteClient.inMemory();

  List<Book> books = [];

  @override
  void initState() {
    super.initState();
    initializeDatabase();
  }

  Future<void> initializeDatabase() async {
    final schema = Schema(
      version: 1,
      tables: [
        Table(
          name: "books",
          columns: [
            Column(name: "id", type: ColumnType.integer, primaryKey: true),
            Column(name: "title", type: ColumnType.text),
            Column(name: "author", type: ColumnType.text),
          ],
        ),
      ],
    );

    await database.setSchema(schema);

    final results = await database.query("SELECT * FROM books");
    final bookRecords = results.toList();

    setState(() {
      books = bookRecords.map((record) {
        return Book(
          id: record["id"],
          title: record["title"],
          author: record["author"],
        );
      }).toList();
    });
  }

  Future<void> addBook(Book book) async {
    await database.insert("books", {
      "id": book.id,
      "title": book.title,
      "author": book.author,
    });

    setState(() {
      books.add(book);
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Book List"),
      ),
      body: ListView.builder(
        itemCount: books.length,
        itemBuilder: (context, index) {
          final book = books[index];
          return ListTile(
            title: Text(book.title),
            subtitle: Text(book.author),
          );
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          final newBook = Book(
            id: books.length + 1,
            title: "New Book",
            author: "Unknown Author",
          );
          addBook(newBook);
        },
        child: Icon(Icons.add),
      ),
    );
  }
}

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter SQL Example',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: BookListScreen(),
    );
  }
}
```

In this example, the `initializeDatabase` method sets up the database and retrieves initial data from the database table "books". The `addBook` method inserts a new book record into the database and updates the UI by adding the book to the list.

## Conclusion

The **flutter_sql** package provides an elegant solution for integrating SQL databases into Flutter applications for local state management. With its simple API and powerful features, you can easily create, read, update, and delete records in a local SQLite database.

By leveraging the capabilities of **flutter_sql**, you can build reactive and performant Flutter applications that efficiently manage local state. Give it a try, and streamline your local state management in Flutter!

## Resources

- [flutter_sql package](https://pub.dev/packages/flutter_sql)
- [SQLite documentation](https://www.sqlite.org/docs.html)

#flutter #SQL