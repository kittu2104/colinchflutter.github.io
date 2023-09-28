---
layout: post
title: "Writing SQL queries for database migrations in Flutter"
description: " "
date: 2023-09-24
tags: [database, migrations]
comments: true
share: true
---

When developing apps with Flutter, one common requirement is managing a local database for storing data. Flutter provides a plugin called `sqflite` which allows us to interact with SQLite databases. SQLite is widely used in mobile app development due to its lightweight and reliable nature.

When working with local databases in Flutter, it's important to be able to perform database migrations. **Database migrations** are the process of modifying the structure of our database, such as adding or removing tables, altering column definitions, or adding indexes. Migrations help us manage the evolution of our database schema over time as our app evolves.

To perform database migrations in Flutter, we need to use SQL queries to modify the structure of the database. Here are some example SQL queries to illustrate different migration scenarios:

## Creating a Table

To create a table in the database, we can execute an SQL `CREATE TABLE` statement. Here's an example of creating a table called `users` with two columns, `id` and `name`:

```sql
CREATE TABLE users (
  id INTEGER PRIMARY KEY,
  name TEXT
);
```

## Modifying a Table

To modify a table, we can use the `ALTER TABLE` statement. For example, let's say we want to add a new column called `age` to the `users` table:

```sql
ALTER TABLE users
ADD COLUMN age INTEGER;
```

## Dropping a Table

If we need to remove a table from the database, we can use the `DROP TABLE` statement. Here's an example of dropping the `users` table:

```sql
DROP TABLE users;
```

## Updating Data

To update the data in a table, we use the `UPDATE` statement. For instance, let's say we want to change the name of a user with `id` 1 to "John Doe":

```sql
UPDATE users
SET name = 'John Doe'
WHERE id = 1;
```

These are just a few examples of the SQL queries we can use for database migrations in Flutter. Depending on your specific requirements, you may need to perform more complex operations like adding indexes, renaming columns, or even creating new tables.

Remember, while writing SQL queries, it's important to properly handle error conditions and ensure data integrity. Also, consider using a database migration library like `sqflite_migration_plan` to help manage and track migrations in a more organized manner.

#flutter #database #migrations