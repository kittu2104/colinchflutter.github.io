---
layout: post
title: "Handling data manipulations during migrations in sqflite"
description: " "
date: 2023-09-24
tags: [sqflite, dart]
comments: true
share: true
---

When working with databases using Sqflite, you may need to perform data manipulations during migrations, such as updating existing records or populating new columns with default values. This ensures that your app's data is properly updated when the database schema changes.

In this article, we'll explore how to handle data manipulations during migrations in Sqflite. We'll cover scenarios like adding a new column, updating existing records, and setting default values for new columns.

## Adding a New Column

To add a new column to an existing table, you can use the `migrate` parameter of the `openDatabase` function in Sqflite. 

```dart
Future<void> migrate(Database db, int oldVersion, int newVersion) async {
  if (newVersion > oldVersion) {
    await db.execute('ALTER TABLE your_table ADD COLUMN new_column TEXT');
  }
}

void main() async {
  final database = openDatabase(
    'your_database.db',
    version: 2,
    onCreate: (db, version) {
      // Create the initial schema here
    },
    onUpgrade: migrate,
    onDowngrade: migrate,
  );

  // Use the migrated database here
}
```

In the above example, the `migrate` function is called whenever the database version is upgraded or downgraded. Inside the `migrate` function, we check if the new version is greater than the old version, and if so, execute an SQL statement to add the new column to the table.

## Updating Existing Records

To update existing records during a migration, you can execute SQL statements using the `execute` method. For example, let's say you want to update all records in a table by appending a string to a specific column.

```dart
Future<void> migrate(Database db, int oldVersion, int newVersion) async {
  if (newVersion > oldVersion) {
    final records = await db.query('your_table');
    
    for (final record in records) {
      final newValue = '${record['column']} updated';
      await db.update(
        'your_table',
        {'column': newValue},
        where: 'id = ?',
        whereArgs: [record['id']]
      );
    }
  }
}
```

In the above example, we query all records from the table and iterate over each one to update the desired column by appending the "updated" string. This ensures that existing records are properly modified during the migration process.

## Setting Default Values for New Columns

When adding a new column to an existing table, you may want to set default values for all existing records. Sqflite does not directly support default values, but you can achieve this by performing a two-step migration.

```dart
Future<void> migrate(Database db, int oldVersion, int newVersion) async {
  if (newVersion > oldVersion) {
    await db.execute('ALTER TABLE your_table ADD COLUMN new_column TEXT');
    
    await db.update(
      'your_table',
      {'new_column': 'default_value'},
    );
  }
}
```

In this example, after adding the new column, we execute an `update` statement to set the default value for all existing records. This ensures that the new column is populated with the desired default value.

## Conclusion

Handling data manipulations during migrations in Sqflite is crucial for keeping your app's data in sync with the database schema changes. By leveraging the `migrate` parameter and SQL statements, you can easily perform tasks like adding new columns, updating existing records, and setting default values.

As your app evolves, make sure to plan and implement migrations carefully to ensure a smooth transition for your users' data.

#sqflite #dart