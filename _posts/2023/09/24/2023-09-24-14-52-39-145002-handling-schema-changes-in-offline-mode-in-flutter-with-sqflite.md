---
layout: post
title: "Handling schema changes in offline mode in Flutter with sqflite"
description: " "
date: 2023-09-24
tags: [Flutter, sqflite]
comments: true
share: true
---

When developing Flutter apps that make use of an offline database, it is important to consider how to handle schema changes. A schema change refers to modifications made to the structure of the database, such as adding or removing tables and columns. 

In Flutter, the `sqflite` package provides an easy-to-use SQLite plugin for offline database management. However, by default, `sqflite` doesn't handle schema changes automatically. In this blog post, we will explore how to manage schema changes while operating in offline mode.

## Detecting Schema Changes

To handle schema changes in `sqflite`, we need to detect if the database schema has been updated or modified. One common approach is to store the database schema version as a parameter in a table, most commonly in a table called 'meta'. 

Here's an example of how to create a 'meta' table with the schema version:

```dart
final String createMetaTableQuery = '''
CREATE TABLE meta (
    id INTEGER PRIMARY KEY,
    version INTEGER
)
''';

await db.execute(createMetaTableQuery);
```

## Managing Schema Changes

When the app starts, we need to check if the database schema version stored in the 'meta' table matches the expected schema version. If they don't match, it means a schema change has occurred, and we need to update the database accordingly.

Here is an example of how to handle schema changes:

```dart
Future<void> _checkSchemaVersion(Database db) async {
  final int expectedSchemaVersion = 2;

  final List<Map<String, dynamic>> result =
      await db.rawQuery('SELECT version FROM meta');

  if (result.isEmpty) {
    // First time setup
    await db.insert('meta', {'version': expectedSchemaVersion});
  } else {
    final int currentSchemaVersion = result.first['version'] as int;

    if (currentSchemaVersion < expectedSchemaVersion) {
      // Perform schema migration
      // ...
      // Update the schema version after migration
      await db.update('meta', {'version': expectedSchemaVersion});
    }
  }
}
```

In the example, we assume that the expected schema version is `2`. We retrieve the current schema version from the 'meta' table and compare it with the expected version. If the current version is lower, we can perform the necessary schema migrations to update the database structure and then update the 'meta' table with the new version.

## Performing Schema Migrations

Schema migration refers to the process of updating the database structure to match the new schema version. This can include tasks such as adding or renaming tables and columns, and transferring existing data to the new structure.

To perform schema migrations, you can use the `sqflite_migration_plan` package. It simplifies the process by providing a way to define migration steps in a structured manner.

Here is an example of how to use `sqflite_migration_plan` to perform a schema migration:

```dart
final MigrationPlan migrationPlan = MigrationPlan(
  // Define schema changes in migration steps
  steps: [
    MigrationStep(1, onCreate: (db) async {
      // Create table version 1
      await db.execute('''
        CREATE TABLE users (
          id INTEGER PRIMARY KEY,
          name TEXT
        )
      ''');
    }),
    MigrationStep(2, onUpgrade: (db, from, to) async {
      // Perform schema migration from version 1 to 2
      // ...
      // Update schema from version 1 to 2
      await db.execute('''
        ALTER TABLE users
        ADD COLUMN email TEXT
      ''');
    }),
  ],
);

await migrationPlan.migrate(db);
```

In the example above, we define a `MigrationPlan` with two migration steps. The `onCreate` callback in the first step defines the initial creation of the 'users' table with version 1 schema. The `onUpgrade` callback in the second step performs the necessary schema migration from version 1 to 2, adding a new 'email' column.

Finally, we call `migrate(db)` on the `MigrationPlan` object to execute the defined migration steps.

## Conclusion

Handling schema changes in offline mode is an important consideration when using `sqflite` in Flutter. By storing and comparing the schema version in a 'meta' table, and using a structured migration plan like `sqflite_migration_plan`, we can effectively manage schema changes in our Flutter app's offline database.

Remember, properly handling schema changes ensures that your app can seamlessly upgrade to new versions without losing important data or encountering database errors along the way.

#Flutter #sqflite