---
layout: post
title: "Integrating JSON serialization with GraphQL client in Flutter"
description: " "
date: 2023-09-27
tags: [Flutter, GraphQL]
comments: true
share: true
---

In Flutter, GraphQL has gained popularity as a modern way to fetch and manage data efficiently. However, handling JSON serialization and deserialization with GraphQL can sometimes be challenging. In this blog post, we will explore how to integrate JSON serialization with a GraphQL client in Flutter.

## What is JSON Serialization?

JSON Serialization is the process of converting an object into a JSON string, which can then be transmitted over the network or stored in a file. In Flutter, the `json_serializable` library makes it easy to serialize and deserialize JSON data.

## Setting up the Project

To get started, create a new Flutter project or open an existing one. Next, add the necessary dependencies to your `pubspec.yaml` file.

```dart
dependencies:
  graphql_flutter: ^5.0.0
  json_serializable: ^5.0.1
  build_runner: ^2.1.4
```

Run `flutter pub get` to fetch the dependencies.

## Generating JSON Serialization Code

To generate JSON serialization code, we need to create a model class and annotate it with the necessary annotations. For example, let's say we have a `Person` class with `name` and `age` attributes.

```dart
import 'package:json_annotation/json_annotation.dart';

part 'person.g.dart';

@JsonSerializable()
class Person {
  final String name;
  final int age;

  Person({
    required this.name,
    required this.age,
  });

  factory Person.fromJson(Map<String, dynamic> json) => _$PersonFromJson(json);
  Map<String, dynamic> toJson() => _$PersonToJson(this);
}
```

The annotations `@JsonSerializable()`, `@JsonKey()`, `@JsonLiteral()` are used to define how the JSON serialization and deserialization should be handled.

## Generating Serialization Code

Next, we need to generate the serialization code using the `build_runner` package. Open a terminal and run the following command:

```
flutter pub run build_runner build
```

This will generate the serialization code in a new file called `person.g.dart`. Make sure to import this file in your code.

## Using JSON Serialization with GraphQL

Now that we have our model class with JSON serialization, let's integrate it with a GraphQL client in Flutter.

First, create a GraphQL client instance.

```dart
import 'package:graphql_flutter/graphql_flutter.dart';

GraphQLClient createGraphQLClient(String url) {
  final HttpLink httpLink = HttpLink(url);
  final Link link = httpLink;

  return GraphQLClient(
    cache: GraphQLCache(),
    link: link,
  );
}
```

Next, define a GraphQL query and call the `QueryOptions` constructor, passing the query and any variables.

```dart
final String query = '''
  query {
    persons {
      name
      age
    }
  }
''';

final QueryOptions options = QueryOptions(
  document: gql(query),
);
```

To execute the query, call the `query` method on the GraphQL client instance.

```dart
final QueryResult result = await client.query(options);

if (result.hasException) {
  print(result.exception);
} else {
  final List<dynamic> jsonData = result.data?['persons'] ?? [];
  final List<Person> persons = jsonData.map((e) => Person.fromJson(e)).toList();

  // Do something with the list of persons
}
```

In the example above, we deserialize the JSON data received from the GraphQL server into a list of `Person` objects using the generated `fromJson` factory method.

## Conclusion

Integrating JSON serialization with a GraphQL client in Flutter is essential for managing data efficiently. By following the steps outlined in this blog post, you can easily integrate JSON serialization into your GraphQL client in Flutter. Remember to use the `json_serializable` library and generate the necessary serialization code using the `build_runner` package. Happy coding!

#Flutter #GraphQL