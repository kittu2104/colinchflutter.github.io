---
layout: post
title: "Using GraphQL APIs in a StatelessWidget in Flutter"
description: " "
date: 2023-09-24
tags: [flutter, graphql]
comments: true
share: true
---

GraphQL is a powerful query language that enables efficient data fetching for client applications. In Flutter, you can easily integrate GraphQL APIs in a `StatelessWidget` to fetch and display data in your user interface. In this blog post, we will explore how to use GraphQL APIs in a `StatelessWidget` in Flutter.

## Installing Dependencies

Before we start, let's make sure we have the necessary dependencies installed. In your Flutter project, open the `pubspec.yaml` file and add the following dependencies:

```dart
dependencies:
  graphql_flutter: ^4.1.0
```

Save the file and run `flutter pub get` to install the dependencies.

## Setting up GraphQL Client

Next, we need to set up a GraphQL client to handle API requests and responses. In Flutter, we can use the `graphql_flutter` package to simplify this process. 

First, import the necessary packages in your Dart file:

```dart
import 'package:flutter/material.dart';
import 'package:graphql_flutter/graphql_flutter.dart';
```

Next, create a `GraphQLClient` instance:

```dart
final HttpLink httpLink = HttpLink('https://api.example.com/graphql');
final GraphQLClient client = GraphQLClient(
  link: httpLink,
  cache: GraphQLCache(),
);
```

Make sure to replace `'https://api.example.com/graphql'` with the actual URL of your GraphQL API.

## Querying Data

Now that we have set up our GraphQL client, we can start querying data from the API. In this example, let's assume we want to fetch a list of posts from our GraphQL API.

Create a new `StatelessWidget` and override the `build` method:

```dart
class PostListWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Query(
      options: QueryOptions(
        document: gql('''
          query {
            posts {
              id
              title
              body
            }
          }
        '''),
      ),
      builder: (QueryResult result, {VoidCallback? refetch, FetchMore? fetchMore}) {
        if (result.hasException) {
          return Text('Error fetching posts!');
        }

        if (result.isLoading) {
          return CircularProgressIndicator();
        }

        final posts = result.data!['posts'];

        return ListView.builder(
          itemCount: posts.length,
          itemBuilder: (BuildContext context, int index) {
            return ListTile(
              title: Text(posts[index]['title']),
              subtitle: Text(posts[index]['body']),
            );
          },
        );
      },
    );
  }
}
```

The `Query` widget from the `graphql_flutter` package wraps our query and provides the necessary options. In the `builder` function, we handle the different states of the query result. If an error occurs, we display an error message. If the data is still loading, we show a loading indicator. Finally, if the data is fetched successfully, we loop through the posts and display them in a `ListView`.

## Using the GraphQL Widget

To use our `PostListWidget` in our main Flutter app, we simply need to wrap it in a `GraphQLProvider` widget. In the `GraphQLProvider`, we pass the `GraphQLClient` instance we created earlier.

```dart
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return GraphQLProvider(
      client: client,
      child: MaterialApp(
        title: 'GraphQL Example',
        theme: ThemeData(
          primarySwatch: Colors.blue,
        ),
        home: Scaffold(
          appBar: AppBar(
            title: Text('GraphQL Example'),
          ),
          body: Center(
            child: PostListWidget(),
          ),
        ),
      ),
    );
  }
}
```

With the `GraphQLProvider` set up, our `PostListWidget` can now access the GraphQL client and query the data from the API.

## Conclusion

In this blog post, we learned how to use GraphQL APIs in a `StatelessWidget` in Flutter. We set up a GraphQL client using the `graphql_flutter` package, performed a query to fetch posts from the API, and displayed the data in a `ListView`. With the power of GraphQL, you can easily integrate and retrieve data from APIs in your Flutter applications.

#flutter #graphql