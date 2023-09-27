---
layout: post
title: "Implementing JSON serialization with graphql_flutter in Flutter"
description: " "
date: 2023-09-27
tags: [GraphQL]
comments: true
share: true
---

GraphQL is a powerful query language that allows efficient data fetching in web and mobile applications. When working with GraphQL in Flutter using the [`graphql_flutter`](https://pub.dev/packages/graphql_flutter) package, it's important to handle JSON serialization to convert the received data into native Dart objects.

In this blog post, we'll explore how to implement JSON serialization with `graphql_flutter` in Flutter, enabling you to seamlessly consume GraphQL APIs and work with structured data in your application.

## Setting up the `graphql_flutter` Package

First, let's add the `graphql_flutter` package to our `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  graphql_flutter: ^3.0.1
  # other dependencies...
```

Run `flutter pub get` to fetch the package and its dependencies.

## Defining GraphQL Queries and Mutations

To query or mutate data using GraphQL, we need to define queries and mutations. `graphql_flutter` provides a convenient way to define GraphQL operations using the `graphql` keyword followed by the GraphQL query or mutation:

```dart
import 'package:graphql_flutter/graphql_flutter.dart';

void main() {
  final HttpLink httpLink = HttpLink(
    uri: 'https://api.example.com/graphql',
  );

  final ValueNotifier<GraphQLClient> client = ValueNotifier<GraphQLClient>(
    GraphQLClient(
      link: httpLink,
      cache: GraphQLCache(),
    ),
  );

  // Querying the GraphQL API
  final query = gql(r'''
    query {
      posts {
        id
        title
        author
      }
    }
  ''');

  // Mutating data in GraphQL API
  final mutation = gql(r'''
    mutation {
      createPost(title: "New Post", author: "John Doe") {
        id
        title
        author
      }
    }
  ''');
}
```

In the above example, we have defined a `query` and a `mutation` using the `gql` function from `graphql_flutter`. The queries and mutations follow GraphQL syntax and define the specific fields we want to fetch or update.

## Serializing JSON Data

To deserialize the JSON data returned by GraphQL queries or mutations into Dart objects, we can define model classes that represent the structure of the received data.

For example, if our GraphQL API returns a list of `Post` objects with `id`, `title`, and `author` fields, we can define the `Post` class as follows:

```dart
class Post {
  final String id;
  final String title;
  final String author;

  Post({required this.id, required this.title, required this.author});
}
```

Once we have defined our model classes, we can use the `fromJson` method from the `json_serializable` package to deserialize the JSON data into native Dart objects:

```dart
import 'package:json_annotation/json_annotation.dart';

part 'post.g.dart';

@JsonSerializable()
class Post {
  final String id;
  final String title;
  final String author;

  Post({required this.id, required this.title, required this.author});

  factory Post.fromJson(Map<String, dynamic> json) => _$PostFromJson(json);
}
```

To generate the necessary serialization code, run the following command in your project directory:

```bash
flutter pub run build_runner build
```

This will generate the `post.g.dart` file, which contains the necessary code for serialization and deserialization.

## Handling JSON Serialization in GraphQL

To integrate the JSON serialization with `graphql_flutter`, we can use the `fromJson` method to convert the received JSON data into native Dart objects.

Here's an example of how we can handle serialization with `graphql_flutter`:

```dart
import 'package:graphql_flutter/graphql_flutter.dart';

void main() {
  // ...

  final GraphQLClient graphqlClient = GraphQLClient(
    link: httpLink,
    cache: GraphQLCache(),
  );

  final options = QueryOptions(
    document: query,
  );

  // Executing the GraphQL query and handling the response
  graphqlClient.query(options).then((result) {
    if (result.hasException) {
      print(result.exception.toString());
    } else {
      final posts = (result.data?['posts'] as List<dynamic>)
          .map((postJson) => Post.fromJson(postJson))
          .toList();

      // Work with deserialized posts...
    }
  });

  // ...
}
```

In the above example, we execute a GraphQL query using `graphql_flutter` and handle the response. We convert the JSON data into a list of `Post` objects using the `fromJson` method, allowing us to work with structured data within our Flutter application.

## Conclusion

By implementing JSON serialization with `graphql_flutter` in Flutter, we can easily consume GraphQL APIs and work with structured data in our applications. With the power of GraphQL and the convenience of JSON serialization, we can build robust and efficient applications.

Remember to define model classes and use the `fromJson` method to deserialize the JSON data received from GraphQL queries or mutations. This will allow you to seamlessly integrate GraphQL into your Flutter app.

#flutter #GraphQL