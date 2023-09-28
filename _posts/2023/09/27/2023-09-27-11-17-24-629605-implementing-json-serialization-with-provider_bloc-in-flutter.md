---
layout: post
title: "Implementing JSON serialization with provider_bloc in Flutter"
description: " "
date: 2023-09-27
tags: [provider_bloc]
comments: true
share: true
---

In Flutter, the provider_bloc package is a popular state management solution that combines the provider package with the bloc pattern. It allows developers to efficiently manage their app's state and separates the business logic from the UI, promoting clean and maintainable code.

When working with APIs, it's common to receive JSON data as responses. To handle this data efficiently, we need to deserialize or convert the JSON into Dart objects. In this blog post, we will explore how to implement JSON serialization with provider_bloc in Flutter.

## Setting Up

1. First, make sure you have the provider_bloc package added to your `pubspec.yaml` file:
   ```yaml
   dependencies:
     provider_bloc: ^x.x.x
   ```

2. Update your dependencies by running:
   ```
   flutter pub get
   ```

3. Import relevant packages in your Dart file:
   ```dart
   import 'dart:convert';
   import 'package:provider_bloc/provider_bloc.dart';
   ```

## Creating Models

Before we can deserialize JSON data, we need to define the models that will represent the data structure. Let's create a simple example with a `User` model:

```dart
class User {
  final int id;
  final String name;
  final String email;

  User({
    required this.id,
    required this.name,
    required this.email,
  });

  factory User.fromJson(Map<String, dynamic> json) {
    return User(
      id: json['id'],
      name: json['name'],
      email: json['email'],
    );
  }
}
```

The `User` class has properties for `id`, `name`, and `email`, along with a factory constructor `fromJson` that takes a JSON map and creates a new instance of the `User` class.

## Deserializing JSON

To deserialize JSON data using provider_bloc, we can create a `Bloc` responsible for fetching and converting the data. Let's create a `UserBloc` that fetches user data from an API:

```dart
class UserBloc extends Bloc {
  final ApiService _apiService = ApiService();

  final _userController = StreamController<User>();

  Stream<User> get userStream => _userController.stream;

  void getUserData() async {
    // Fetch data from API
    final response = await _apiService.getUserData();

    // Deserialize JSON using User.fromJson constructor
    final userData = User.fromJson(json.decode(response.body));

    // Add the deserialized user data to the stream
    _userController.sink.add(userData);
  }

  @override
  void dispose() {
    _userController.close();
  }
}
```

In this example, we have a `getUserData` method that makes an API call to fetch user data. Once we receive the response, we deserialize the JSON using the `User.fromJson` constructor and add the deserialized data to a stream.

## Consuming the UserBloc

Now that we have the `UserBloc`, we can consume it in our UI using the `Provider` widget from the provider package. Let's create a simple widget that displays the user's name:

```dart
class UserNameWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final userBloc = Provider.of<UserBloc>(context);

    return StreamBuilder<User>(
      stream: userBloc.userStream,
      builder: (context, snapshot) {
        if (snapshot.hasData) {
          final user = snapshot.data!;
          return Text(
            user.name,
            style: TextStyle(fontSize: 18),
          );
        } else {
          return Text('Loading...');
        }
      },
    );
  }
}
```

In this widget, we use the `StreamBuilder` widget to listen to changes in the `userStream` and update the UI accordingly. When we have data, we display the user's name, and when the data is loading, we display a loading indicator.

## Conclusion

By implementing JSON serialization with provider_bloc in Flutter, we can efficiently handle API responses and convert them into Dart objects. This promotes clean code separation and makes our apps more maintainable. With the help of the provider_bloc package, managing app state and business logic becomes much easier.

Remember to always handle exceptions and errors when deserializing JSON and make necessary validations for the incoming data to ensure a smooth app experience.

#flutter #provider_bloc