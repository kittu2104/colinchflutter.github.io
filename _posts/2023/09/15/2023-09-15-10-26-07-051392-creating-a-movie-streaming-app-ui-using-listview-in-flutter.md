---
layout: post
title: "Creating a movie streaming app UI using ListView in Flutter."
description: " "
date: 2023-09-15
tags: [moviestreamingapp]
comments: true
share: true
---

![Flutter Logo](https://flutter.dev/assets/images/shared/brand/flutter/logo/flutter-lockup.png)

With the increasing popularity of movie streaming apps, it's important for developers to create a user-friendly and visually appealing UI to attract and engage users. In this tutorial, we will learn how to create a movie streaming app UI using the ListView widget in Flutter.

## Prerequisites

Before we begin, make sure you have Flutter installed on your machine. You can follow the official Flutter installation guide to set up Flutter: [Install Flutter](https://flutter.dev/docs/get-started/install)

## Step 1: Set up a new Flutter project

First, let's create a new Flutter project by running the following command in your terminal:

```bash
flutter create movie_streaming_app
cd movie_streaming_app
```

## Step 2: Create the movie list view

Open the `lib/main.dart` file and replace the code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MovieStreamingApp());
}

class MovieStreamingApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Movie Streaming App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: MovieListPage(),
    );
  }
}

class MovieListPage extends StatelessWidget {
  final List<String> movies = [
    'Inception',
    'The Shawshank Redemption',
    'The Matrix',
    'Pulp Fiction',
    'Fight Club',
    'The Dark Knight',
    'Interstellar',
    'The Godfather',
    'Goodfellas',
    'Schindler\'s List',
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Movies'),
      ),
      body: ListView.builder(
        itemCount: movies.length,
        itemBuilder: (context, index) {
          return ListTile(
            title: Text(movies[index]),
          );
        },
      ),
    );
  }
}
```

In the `MovieListPage` widget, we have a list of movies and we use the `ListView.builder` widget to display the movies as a list of `ListTile` widgets.

## Step 3: Run the app

To run the app on your emulator or device, use the following command:

```bash
flutter run
```

You should now see a movie streaming app with a list of movies on the screen.

## Conclusion

In this tutorial, we learned how to create a movie streaming app UI using the ListView widget in Flutter. The ListView widget is a powerful tool for creating scrollable lists with great performance and flexibility.

Remember, this is just the beginning. You can further enhance the UI by customizing the list item widgets and integrating with your own movie data. Feel free to explore the Flutter documentation for more information and possibilities.

#flutter #moviestreamingapp