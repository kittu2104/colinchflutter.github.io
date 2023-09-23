---
layout: post
title: "Working with local databases in Flutter WebAssembly"
description: " "
date: 2023-09-24
tags: [flutter, webassembly]
comments: true
share: true
---

Flutter is a popular framework for building cross-platform apps, and recently it has gained support for WebAssembly, allowing developers to run Flutter applications in the web browser. One of the common requirements in app development is the need to store data locally on the device. In this blog post, we'll explore how to work with local databases in Flutter WebAssembly.

## Setting Up the Project

To get started, make sure you have Flutter installed on your machine. Then, create a new Flutter project by running the following command:

```bash
flutter create local_database_example
```

Next, navigate into the project directory:

```bash
cd local_database_example
```

## Installing Dependencies

To work with local databases in Flutter WebAssembly, we will be using the `sembast` package. Open the `pubspec.yaml` file and add the following dependency:

```yaml
dependencies:
  sembast: ^3.0.0
```

Save the file and run the following command to install the package:

```bash
flutter pub get
```

## Creating the Database

In Flutter WebAssembly, we can create and manage local databases using the `sembast` package. First, import the necessary libraries at the top of your Dart file:

```dart
import 'package:sembast/sembast.dart';
import 'package:sembast/sembast_io.dart';
```

Next, define a function to open the database and create a store:

```dart
Future<Database> _openDatabase() async {
  final appDocumentDir = await getApplicationDocumentsDirectory();
  final dbPath = join(appDocumentDir.path, 'local_database.db');
  final database = await databaseFactoryIo.openDatabase(dbPath);
  return database;
}
```

In the above code, we use the `getApplicationDocumentsDirectory()` function from the `path_provider` package to get the path where the database file will be stored.

## CRUD Operations

With the database set up, we can now perform CRUD (Create, Read, Update, Delete) operations on the local database.

### Creating a Record

To create a new record in the database, use the following code:

```dart
final database = await _openDatabase();
final store = intMapStoreFactory.store('records');
final newRecord = {'name': 'John Doe', 'age': 30};
await store.add(database, newRecord);
```

### Reading Records

To read records from the database, use the following code:

```dart
final database = await _openDatabase();
final store = intMapStoreFactory.store('records');
final recordsSnapshot = await store.find(database);
final records = recordsSnapshot.map((snapshot) => snapshot.value).toList();
```

### Updating a Record

To update an existing record in the database, use the following code:

```dart
final database = await _openDatabase();
final store = intMapStoreFactory.store('records');
final updatedRecord = {'name': 'Jane Smith', 'age': 32};
await store.update(database, updatedRecord, finder: Finder(filter: Filter.byKey(recordId)));
```

In the above code, `recordId` is the unique identifier of the record.

### Deleting a Record

To delete a record from the database, use the following code:

```dart
final database = await _openDatabase();
final store = intMapStoreFactory.store('records');
await store.delete(database, finder: Finder(filter: Filter.byKey(recordId)));
```

## Conclusion

In this blog post, we learned how to work with local databases in Flutter WebAssembly. We explored how to set up a database, perform CRUD operations, and manage records. Using local databases can greatly improve the user experience of your Flutter apps by allowing them to store and retrieve data locally. Get started with Flutter WebAssembly and leverage the power of local databases to build responsive and feature-rich web applications.

#flutter #webassembly