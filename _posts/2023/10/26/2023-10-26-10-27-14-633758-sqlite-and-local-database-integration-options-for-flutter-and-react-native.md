---
layout: post
title: "SQLite and local database integration options for Flutter and React Native"
description: " "
date: 2023-10-26
tags: [reactnative]
comments: true
share: true
---

In modern app development, it is common to store data locally on the user's device for offline access and optimized performance. SQLite, a lightweight and open-source relational database, is often the go-to choice for this purpose due to its simplicity and excellent cross-platform support. In this blog post, we will explore the SQLite integration options available for two popular cross-platform frameworks, Flutter and React Native.

## SQLite Integration in Flutter

### sqflite package

Flutter has excellent SQLite support through the sqflite package, which provides a high-level API for working with SQLite databases. This package offers convenient methods for creating, querying, and updating tables, making it easy to manage local data storage within your Flutter apps.

To use sqflite, add it as a dependency in your pubspec.yaml file:

```dart
dependencies:
  sqflite: ^2.0.0+4
  path: ^2.1.0
```

Here is an example of how you can use sqflite to create a database and perform some basic operations:

```dart
import 'package:sqflite/sqflite.dart';
import 'package:path/path.dart';

void main() async {
  
  // Define database path
  String path = join(await getDatabasesPath(), 'my_database.db');

  // Open the database
  Database database = await openDatabase(
    path,
    version: 1,
    onCreate: (db, version) {
      // Create tables
      db.execute('CREATE TABLE users (id INTEGER PRIMARY KEY, name TEXT)');
    },
  );

  // Insert data
  await database.insert('users', {'id': 1, 'name': 'John'});

  // Query data
  List<Map<String, dynamic>> users = await database.query('users');

  // Update data
  await database.update('users', {'name': 'John Doe'}, where: 'id = ?', whereArgs: [1]);
  
  // Delete data
  await database.delete('users', where: 'id = ?', whereArgs: [1]);

  // Close the database
  await database.close();
}
```

### Moor package

Another popular option for SQLite integration in Flutter is the moor package. Moor takes a different approach by using code generation to build a type-safe API for your database. It offers a fluent query API and supports advanced features like database migrations.

To use moor, add it as a dependency in your pubspec.yaml file:

```dart
dependencies:
  moor: ^4.4.0
```

Here is an example of how you can use moor to define a database and perform some basic operations:

```dart
import 'package:moor/moor.dart';
import 'package:moor_flutter/moor_flutter.dart';

part 'my_database.g.dart';

class Users extends Table {
  IntColumn get id => integer().autoIncrement()();
  TextColumn get name => text()();
}

@UseMoor(tables: [Users])
class MyDatabase extends _$MyDatabase {
  MyDatabase() : super((FlutterQueryExecutor.inDatabaseFolder(path: 'my_database.db')));

  @override
  int get schemaVersion => 1;
}

void main() async {
  MyDatabase database = MyDatabase();

  // Insert data
  await database.into(database.users).insert(UsersCompanion.insert(name: 'John'));

  // Query data
  List<User> users = await database.select(database.users).get();

  // Update data
  await database.update(database.users).replace(User(id: 1, name: 'John Doe'));

  // Delete data
  await database.delete(database.users).delete(User(id: 1));

  // Close the database
  await database.close();
}
```

## SQLite Integration in React Native

### react-native-sqlite-storage package

For React Native, the react-native-sqlite-storage package provides a way to integrate SQLite databases into your applications. This package supports both iOS and Android platforms, allowing you to utilize SQLite's power on both platforms.

To use react-native-sqlite-storage, install it using npm or yarn:

```
npm install react-native-sqlite-storage
```

Here is an example of how you can use react-native-sqlite-storage to create a database and perform some basic operations in React Native:

```javascript
import SQLite from 'react-native-sqlite-storage';

// Create or open the database
const db = SQLite.openDatabase({ name: 'my_database.db' });

// Execute SQL statement to create a table
db.transaction((tx) => {
  tx.executeSql('CREATE TABLE IF NOT EXISTS users (id INTEGER PRIMARY KEY, name TEXT)');
});

// Insert data
db.transaction((tx) => {
  tx.executeSql('INSERT INTO users (id, name) VALUES (?, ?)', [1, 'John']);
});

// Query data
db.transaction((tx) => {
  tx.executeSql('SELECT * FROM users', [], (tx, results) => {
    const users = results.rows.raw();
    console.log(users);
  });
});

// Update data
db.transaction((tx) => {
  tx.executeSql('UPDATE users SET name = ? WHERE id = ?', ['John Doe', 1]);
});

// Delete data
db.transaction((tx) => {
  tx.executeSql('DELETE FROM users WHERE id = ?', [1]);
});

// Close the database
db.close();
```

### AsyncStorage

Another option for local data storage in React Native is the AsyncStorage API, which provides a simple key-value storage mechanism. Although not as powerful as SQLite, AsyncStorage is lightweight and suitable for smaller data storage requirements.

Here is an example of how you can use AsyncStorage to perform basic operations:

```javascript
import AsyncStorage from '@react-native-async-storage/async-storage';

// Insert data
AsyncStorage.setItem('user', JSON.stringify({ id: 1, name: 'John' }));

// Retrieve data
AsyncStorage.getItem('user').then((value) => {
  const user = JSON.parse(value);
  console.log(user);
});

// Update data
AsyncStorage.setItem('user', JSON.stringify({ id: 1, name: 'John Doe' }));

// Delete data
AsyncStorage.removeItem('user');
```

## Conclusion

Both Flutter and React Native provide excellent options for integrating SQLite and local databases into your cross-platform apps. The sqflite and moor packages in Flutter, and the react-native-sqlite-storage package and AsyncStorage in React Native, offer powerful and easy-to-use solutions for managing local data storage. Choose the option that best fits your app's requirements and enjoy the benefits of offline data access and improved performance.

Remember to use the appropriate package documentation and resources to further explore the capabilities and advanced features of SQLite integration in Flutter and React Native.

#flutter #reactnative