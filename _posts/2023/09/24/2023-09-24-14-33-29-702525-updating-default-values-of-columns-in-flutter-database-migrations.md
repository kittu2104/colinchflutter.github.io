---
layout: post
title: "Updating default values of columns in Flutter database migrations"
description: " "
date: 2023-09-24
tags: [databasemigrations]
comments: true
share: true
---

When working with a database in your Flutter application, it's common to make changes to the database schema over time. One such change is updating the default values of columns in existing tables. In this blog post, we will explore how to accomplish this using database migrations in Flutter.

## What are database migrations?

Database migrations are a way to make changes to the structure or schema of a database without losing its data. They allow you to update tables, add or remove columns, modify constraints, and perform other changes necessary to keep your database up-to-date with the evolving needs of your application.

## Updating default values with migrations

To update the default value of a column in an existing table, we will need to create a new migration file and use the `ALTER TABLE` statement in SQL to modify the default value.

### Step 1: Create a new migration file

In your Flutter project, navigate to the `migrations` directory under the `database` directory. If the `migrations` directory does not exist, create it manually. Within the `migrations` directory, create a new migration file, for example, `20220101000000_update_default_value.dart`. The name of the migration file should follow a timestamp format to ensure the order of execution.

### Step 2: Write the migration code

Inside the newly created migration file, override the `up` method and use the following syntax to update the default value of a column:

```dart
class UpdateDefaultValue extends Migration {
  @override
  Future<void> up() async {
    database.execute("ALTER TABLE table_name MODIFY column_name DEFAULT new_default_value;");
  }

  @override
  Future<void> down() async {
    // Optional: Write the down migration to revert the changes if necessary
  }
}
```

Replace `table_name` with the name of the table you want to update, `column_name` with the name of the specific column, and `new_default_value` with the desired new default value.

### Step 3: Run the migration

To apply the migration and update the default value, run the following command in your terminal:

```
flutter pub run build_runner build --delete-conflicting-outputs
```

This command will generate the necessary code and run the migration.

## Conclusion

By following these steps, you can easily update the default values of columns in Flutter database migrations. Keep in mind that database migrations are essential for maintaining the integrity and consistency of your database as your application evolves. They allow you to make changes to the schema while preserving your data.

#flutter #databasemigrations