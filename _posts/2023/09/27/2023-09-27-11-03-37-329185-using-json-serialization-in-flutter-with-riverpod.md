---
layout: post
title: "Using JSON serialization in Flutter with Riverpod"
description: " "
date: 2023-09-27
tags: []
comments: true
share: true
---

In Flutter, the **Riverpod** library provides a simple and efficient way to manage state in your application. When working with APIs or database communication, it often involves dealing with data in **JSON** format. **JSON** serialization is the process of converting **Dart objects** into JSON strings and vice versa. In this article, we will explore how to use JSON serialization with **Riverpod** in Flutter.

## Step 1: Adding Dependencies

First, you need to add the necessary dependencies to your `pubspec.yaml` file. Open the `pubspec.yaml` file and add the following dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter
  riverpod: ^1.0.0

dev_dependencies:
  json_serializable: ^5.0.0
  build_runner: ^2.0.0
```

Save the file and run `flutter pub get` in your terminal to fetch the updated dependencies.

## Step 2: Creating Data Model

Next, let's create a **data model** class representing the object we want to serialize. As an example, let's create a `User` class with `id`, `name`, and `email` fields.

```dart
import 'package:json_annotation/json_annotation.dart';

part 'user.g.dart';

@JsonSerializable()
class User {
  final int id;
  final String name;
  final String email;

  User(this.id, this.name, this.email);

  factory User.fromJson(Map<String, dynamic> json) => _$UserFromJson(json);
  Map<String, dynamic> toJson() => _$UserToJson(this);
}
```

In the above code, we use the `json_annotation` package to provide annotations for the serialization process. The `@JsonSerializable` annotation is added to the class. It indicates that this class should be considered for JSON serialization. The `toJson()` and `fromJson()` methods are automatically generated using the build_runner.

## Step 3: Generating Serialization Code

Now, we need to generate the serialization code for our `User` class. Open your terminal and run the following command:

```bash
flutter pub run build_runner build
```

This command will generate the necessary serialization code in a new file named `user.g.dart`.

## Step 4: Using Riverpod with JSON Serialization

To use **Riverpod** with JSON serialization, we can create a **provider** that loads data from a JSON file and returns a list of users.

```dart
import 'package:flutter_riverpod/flutter_riverpod.dart';
import 'package:flutter/services.dart' show rootBundle;
import 'dart:convert';

final usersProvider = FutureProvider<List<User>>((ref) async {
  final jsonString = await rootBundle.loadString('assets/users.json');
  final jsonData = json.decode(jsonString) as List<dynamic>;
  return jsonData.map((item) => User.fromJson(item)).toList();
});
```

In the above code, we define a **future provider** named `usersProvider` that loads the JSON data from a file named `users.json`. We use the `rootBundle` method to load the JSON string, then parse it using `json.decode()`. Finally, we map the JSON objects to our `User` class using the `User.fromJson` factory method.

## Step 5: Consuming the Data

To consume the users data, we can use the `useProvider` hook provided by **Riverpod**. Here's an example of how to display a list of users:

```dart
class UserListPage extends ConsumerWidget {
  @override
  Widget build(BuildContext context, ScopedReader watch) {
    final users = watch(usersProvider);

    return users.when(
      data: (userList) => ListView.builder(
        itemCount: userList.length,
        itemBuilder: (context, index) {
          final user = userList[index];
          return ListTile(
            title: Text(user.name),
            subtitle: Text(user.email),
          );
        },
      ),
      loading: () => CircularProgressIndicator(),
      error: (error, stackTrace) => Text('Error loading users data.'),
    );
  }
}
```

In the above code, we use the `usersProvider` as the value for `watch`, which will listen for changes in the users data. We then handle the different states of the data using the `users.when` method.

That's it! You have successfully used JSON serialization with **Riverpod** in your Flutter application. By combining **Riverpod** for state management and JSON serialization, you can efficiently handle API data and make it ready for use in your application.