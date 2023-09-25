---
layout: post
title: "Handling null and non-null column changes in Flutter migrations"
description: " "
date: 2023-09-24
tags: [FlutterMigrations]
comments: true
share: true
---

Migrations play a vital role in managing changes to your database schema in Flutter apps. Sometimes, you may need to modify a column to allow null values or make it non-null. In this blog post, we will explore how to handle null and non-null column changes in Flutter migrations.

## Nullable to Non-Nullable Columns

When you want to convert a nullable column to a non-nullable column, you need to ensure that all existing rows have valid non-null values for that column. Otherwise, the migration will fail.

To handle this scenario, you can perform the following steps:

1. Create a new non-nullable column with a temporary name. Make sure to give it an appropriate default value.

   ```dart
   class AddNewColumnMigration extends Migration {
     @override
     Future<void> up(Schema schema) async {
       schema
           .table('your_table')
           .addColumn(Column('new_column_temp', String).nullable().withDefault(''));
     }

     @override
     Future<void> down(Schema schema) async {
       schema.table('your_table').removeColumn('new_column_temp');
     }
   }
   ```

2. Migrate the data from the old nullable column to the new non-nullable column.

   ```dart
   class MigrateDataMigration extends Migration {
     @override
     Future<void> up(Schema schema) async {
       final query =
           'UPDATE your_table SET new_column_temp = old_column WHERE old_column IS NOT NULL;';
       await databaseAdapter.execute(query);
     }

     @override
     Future<void> down(Schema schema) async {
       final query =
           'UPDATE your_table SET old_column = new_column_temp WHERE new_column_temp IS NOT NULL;';
       await databaseAdapter.execute(query);
     }
   }
   ```

3. Remove the old nullable column and rename the temporary column to the original column name.

   ```dart
   class RemoveOldColumnMigration extends Migration {
     @override
     Future<void> up(Schema schema) async {
       schema.table('your_table').removeColumn('old_column');
       schema.table('your_table').renameColumn('new_column_temp', 'old_column');
     }

     @override
     Future<void> down(Schema schema) async {
       schema.table('your_table').renameColumn('old_column', 'new_column_temp');
       schema
           .table('your_table')
           .addColumn(Column('old_column', String).nullable().withDefault(''));
     }
   }
   ```

## Non-Nullable to Nullable Columns

Converting a non-nullable column to nullable is a straightforward process, as there are no data integrity concerns. You can directly modify the column definition in the migration.

```dart
class NullableColumnMigration extends Migration {
  @override
  Future<void> up(Schema schema) async {
    schema
        .table('your_table')
        .alterColumn('your_column', (c) => c..nullable = true);
  }

  @override
  Future<void> down(Schema schema) async {
    schema
        .table('your_table')
        .alterColumn('your_column', (c) => c..nullable = false);
  }
}
```

By following these steps, you can handle null and non-null column changes effectively in Flutter migrations. Remember to thoroughly test your migrations before deploying them to production.

#Flutter #FlutterMigrations