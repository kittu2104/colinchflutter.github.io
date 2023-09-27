---
layout: post
title: "Implementing JSON serialization with GraphQL in Flutter"
description: " "
date: 2023-09-27
tags: [JSONserialization, GraphQL]
comments: true
share: true
---

In this blog post, we will explore how to implement JSON serialization with GraphQL in Flutter. JSON serialization is an essential part of any app that communicates with a server using GraphQL. It allows us to convert JSON data into strongly-typed objects, making it easier to work with the data in our Flutter app.

## What is JSON Serialization?

JSON (JavaScript Object Notation) serialization is the process of converting JSON data into a structured format that can be easily understood and used by programming languages. In the context of Flutter and GraphQL, JSON serialization is used to convert the response from a GraphQL query into Dart objects.

## Setting up Flutter GraphQL

To get started, we need to add the necessary dependencies to our Flutter project. Open the `pubspec.yaml` file and add the following dependencies:

```
dependencies:
  graphql_flutter: ^4.0.0
  json_annotation: ^4.0.0
  build_runner: ^2.0.0
```

Next, run `flutter pub get` to fetch the new dependencies.

## Generating Model Classes

To generate the model classes for our GraphQL data, we'll use a code generation package called `json_serializable`. Add the following lines to your `pubspec.yaml` file:

```
dev_dependencies:
  build_runner: ^2.0.0
  json_serializable: ^6.0.0
```

Now, create a new directory called `models` at the root of your Flutter project. Inside the `models` directory, create a new file called `user.dart`. Add the following code:

```dart
import 'package:json_annotation/json_annotation.dart';

part 'user.g.dart';

@JsonSerializable()
class User {
  final String id;
  final String name;
  final int age;

  User({required this.id, required this.name, required this.age});

  factory User.fromJson(Map<String, dynamic> json) =>
      _$UserFromJson(json);

  Map<String, dynamic> toJson() => _$UserToJson(this);
}
```

Here we have defined a `User` class and used the `@JsonSerializable()` annotation to generate the necessary serialization code. To generate the serialization code, run the following command in your terminal:

```
flutter pub run build_runner build
```

The generated files `user.g.dart` and `user.g.dart.json` should be visible in the `lib/models` directory.

## Using the Generated Model Classes

Now that we have generated the model classes, we can use them to deserialize the GraphQL response. Here's an example of how to do it:

```dart
import 'package:flutter/material.dart';
import 'package:graphql_flutter/graphql_flutter.dart';
import 'package:your_project_name/models/user.dart';

class UserList extends StatelessWidget {
  final String query = '''
    query {
      users {
        id
        name
        age
      }
    }
  ''';

  @override
  Widget build(BuildContext context) {
    return GraphQLConsumer(
      builder: (GraphQLClient client) {
        return Query(
          options: QueryOptions(
            document: gql(query),
          ),
          builder: (QueryResult result, {VoidCallback? refetch}) {
            if (result.hasException) {
              return Text(result.exception.toString());
            }

            if (result.isLoading) {
              return CircularProgressIndicator();
            }

            final List<dynamic> data = result.data?['users'];

            List<User> users =
                data?.map((json) => User.fromJson(json))?.toList() ?? [];

            return ListView.builder(
              itemCount: users.length,
              itemBuilder: (BuildContext context, int index) {
                return ListTile(
                  title: Text(users[index].name),
                  subtitle: Text(users[index].age.toString()),
                );
              },
            );
          },
        );
      },
    );
  }
}
```

In the example above, we are querying for a list of users and deserializing the response using the generated `User` model class. We can then display the users in a `ListView` widget.

## Conclusion

In this blog post, we have explored how to implement JSON serialization with GraphQL in Flutter. We have learned how to generate model classes using `json_serializable` and how to use them to deserialize GraphQL responses. By implementing JSON serialization, we can work with GraphQL data in a more convenient and type-safe manner.

#flutter #JSONserialization #GraphQL #FlutterTutorial