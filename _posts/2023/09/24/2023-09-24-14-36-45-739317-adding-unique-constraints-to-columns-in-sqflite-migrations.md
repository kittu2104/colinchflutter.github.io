---
layout: post
title: "Adding unique constraints to columns in sqflite migrations"
description: " "
date: 2023-09-24
tags: [flutter, sqflite]
comments: true
share: true
---

When working with SQLite databases in Flutter using the `sqflite` package, you may come across scenarios where you need to enforce unique values in certain columns of your database table. Adding unique constraints ensures that no two rows can have the same value in the specified column.

To add a unique constraint to a column in a SQLite table using `sqflite` migrations, you can follow these steps:

1. Open your database migration file. This is typically a .dart file where you define the database schema and migrations.

2. Find the `createTable` method where you specify the columns and their data types for creating the table.

   ```dart
   void _createExampleTable(Database db) {
     db.execute('''
       CREATE TABLE example (
         id INTEGER PRIMARY KEY,
         name TEXT,
         email TEXT
       )
     ''');
   }
   ```

3. Modify the column definition where you want to add the unique constraint. Append the keyword `UNIQUE` after the column name.

   ```dart
   void _createExampleTable(Database db) {
     db.execute('''
       CREATE TABLE example (
         id INTEGER PRIMARY KEY,
         name TEXT UNIQUE, -- Unique constraint added to the 'name' column
         email TEXT
       )
     ''');
   }
   ```

4. If you're adding a unique constraint to an existing table, you need to handle potential duplicate values. SQLite will raise an exception if inserting a new row violates the unique constraint. To avoid this, you can remove or update existing duplicate values before adding the constraint.

5. Run the database migration using `sqflite` migration utilities. This will create or modify the table to include the unique constraint.

With the unique constraint added, SQLite will automatically enforce uniqueness on the specified column, preventing duplicate values from being inserted.

It's important to note that adding unique constraints to columns in an existing table may require extra steps to handle potential duplicates. Additionally, if your application logic relies on these constraints, you should handle the exceptions raised by SQLite appropriately.

#flutter #sqflite