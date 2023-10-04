---
layout: post
title: "Working with databases and local storage in Flutter using GetX"
description: " "
date: 2023-09-29
tags: [GetX, database, localstorage]
comments: true
share: true
---

Flutter is a powerful framework for building cross-platform applications. When working with data in Flutter, it is common to need a way to persist and retrieve information using a database or local storage. In this blog post, we will explore how to work with databases and local storage in Flutter using the GetX package.

### Why use GetX?

GetX is a state management package for Flutter that provides a variety of features, including reactive programming, dependency injection, and route management. It also has a simple and intuitive API for working with databases and local storage. By using GetX, we can easily manage our application's data without relying on external libraries or complex configurations.

### Setting Up GetX

To get started, we need to add the GetX package to our Flutter project's dependencies. Open the `pubspec.yaml` file and add the following line within the `dependencies` section:

```dart
dependencies:
  get: ^4.3.8
```

Next, run `flutter pub get` to fetch the package and update your project.

### Working with Local Storage

GetX provides the `GetStorage` class for working with local storage. To begin using local storage, we need to initialize an instance of `GetStorage` in our application, typically in the `main()` function or a dedicated initialization file.

```dart
import 'package:get_storage/get_storage.dart';

void main() {
  GetStorage.init();
  // Rest of the main function
}
```

Once initialized, we can start using local storage to store and retrieve data. Here's an example of saving and retrieving a value from local storage:

```dart
import 'package:get_storage/get_storage.dart';

void saveData(String key, String value) {
  final box = GetStorage();
  box.write(key, value);
}

String retrieveData(String key) {
  final box = GetStorage();
  return box.read(key);
}
```

### Working with Databases

GetX provides a lightweight, yet powerful, database management solution called `GetXDB`. It has support for both SQL and NoSQL databases. To use `GetXDB`, we need to add the following line to our `pubspec.yaml` file:

```dart
dependencies:
  get_storage: ^2.0.3+6
  get_storage_sqlite: ^1.0.4
```

With `GetXDB`, we can easily create, query, and manipulate databases in our Flutter application. The API is similar to working with local storage, making it easy to transition between the two.

Here's an example of creating a table and inserting data into it using `GetXDB`:

```dart
import 'package:get/get.dart';

class User {
  final String name;
  final int age;

  User({required this.name, required this.age});
}

class UserController extends GetxController {
  final database = GetXDB();

  Future<void> createUser(User user) async {
    await database.createTable('users', ['name', 'age']);
    await database.insert('users', {'name': user.name, 'age': user.age});
  }
}

void main() {
  final userController = UserController();
  final user = User(name: 'John Doe', age: 25);
  userController.createUser(user);
}
```

In the example above, we create a `User` class and a `UserController` class. Inside the `createUser()` method, we create a table called 'users' with two columns, 'name' and 'age'. We then insert the user's name and age into the 'users' table.

### Conclusion

In this blog post, we explored how to work with databases and local storage in Flutter using the GetX package. GetX provides an easy-to-use API for managing local data, allowing us to save and retrieve information from local storage. Additionally, `GetXDB` simplifies working with databases, enabling us to create tables, insert data, and perform queries seamlessly. With GetX, data management becomes a breeze in Flutter applications.

#flutter #GetX #database #localstorage