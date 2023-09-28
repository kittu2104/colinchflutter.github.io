---
layout: post
title: "Implementing JSON serialization with flutter_bloc in Flutter"
description: " "
date: 2023-09-27
tags: []
comments: true
share: true
---

Flutter is a powerful UI toolkit for building beautiful and responsive cross-platform applications. When working with APIs, data is usually exchanged in JSON format. In this article, we will explore how to implement JSON serialization with `flutter_bloc` in Flutter.

## What is flutter_bloc?

`flutter_bloc` is a package that provides a predictable state management solution for Flutter applications. It helps to manage the state of your application using the BLoC (Business Logic Component) pattern. This pattern separates the UI from the business logic and provides a clear separation of concerns.

## Why JSON Serialization?

When consuming API data, it's essential to convert the JSON response into a usable format within the application. JSON serialization allows the conversion of JSON objects into Dart objects, making them easy to work with and manipulate.

## Implementation

To demonstrate JSON serialization with `flutter_bloc`, let's assume we have an API endpoint that returns a list of books in JSON format, like this:

```json
[
    {
        "title": "Flutter in Action",
        "author": "Eric Windmill",
        "category": "Technology"
    },
    {
        "title": "Clean Code",
        "author": "Robert C. Martin",
        "category": "Programming"
    }
    // Additional book objects
]
```

### Step 1: Model Class

First, we need to create a Dart model class representing the book object. Create a new file called `book_model.dart` and add the following code:

```dart
class Book {
  final String title;
  final String author;
  final String category;

  Book({this.title, this.author, this.category});
  
  factory Book.fromJson(Map<String, dynamic> json) {
    return Book(
      title: json['title'],
      author: json['author'],
      category: json['category'],
    );
  }
}
```

In this code, we define a `Book` class with properties `title`, `author`, and `category`. We also add a factory constructor `fromJson` to convert JSON objects into `Book` objects.

### Step 2: Bloc Implementation

Next, let's create a `BookBloc` class to handle the business logic and state management. Create a new file called `book_bloc.dart` and add the following code:

```dart
import 'package:flutter_bloc/flutter_bloc.dart';

class BookBloc extends Bloc<dynamic, List<Book>> {
  @override
  List<Book> get initialState => [];

  @override
  Stream<List<Book>> mapEventToState(dynamic event) async* {
    // Fetch books from API and convert to List<Book>
    List<Book> books = await _fetchBooks();

    yield books;
  }

  Future<List<Book>> _fetchBooks() async {
    // Fetch JSON response from API
    String jsonResponse = await _fetchJsonFromApi();

    // Parse JSON to List<Book>
    List<dynamic> jsonData = json.decode(jsonResponse);
    List<Book> books = jsonData.map((json) => Book.fromJson(json)).toList();

    return books;
  }
}
```

In this code, we define the `BookBloc` class by extending the `Bloc` class from `flutter_bloc`. We override `initialState` to return an empty list of books and implement the `mapEventToState` method to fetch the books from the API and emit the converted `Book` objects as the new state.

### Step 3: Consuming the Bloc

To consume the `BookBloc` in our UI, we need to create a `BlocProvider`. Modify your widget's build method to include the following code:

```dart
BlocProvider<BookBloc>(
  create: (context) => BookBloc(),
  child: MaterialApp(
    // Your app code
  ),
);
```

Now, in the widget where you want to consume the `BookBloc`, add the `BlocBuilder` widget as follows:

```dart
BlocBuilder<BookBloc, List<Book>>(
  builder: (context, books) {
    // Build your UI here using the received books
    // books is a List<Book> object

    return ListView(
      children: books.map((book) => ListTile(title: Text(book.title))).toList(),
    );
  },
);
```

In this code, the `BlocBuilder` listens for state changes from the `BookBloc` and rebuilds the UI whenever the state changes. We map the received books into `ListTile` widgets to display the book titles in a `ListView`.

## Conclusion

JSON serialization is a crucial part of working with APIs in Flutter. By implementing JSON serialization with `flutter_bloc`, we can easily convert JSON objects into Dart objects, making them easy to work with in our Flutter application. Using the `flutter_bloc` package provides a structured approach to state management, ensuring clean separation of concerns and maintainability.