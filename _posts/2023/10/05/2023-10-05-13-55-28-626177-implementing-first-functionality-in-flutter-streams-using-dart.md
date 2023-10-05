---
layout: post
title: "Implementing first functionality in Flutter streams using Dart"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In Flutter, **streams** are a powerful tool for handling asynchronous data streams. They allow you to respond to events or changes in your data in real-time. In this tutorial, we will walk you through implementing your first functionality using **streams** in Flutter using the Dart programming language.

## Table of Contents
- [Introduction to Streams](#introduction-to-streams)
- [Creating a Stream](#creating-a-stream)
- [Adding Stream Listeners](#adding-stream-listeners)
- [Using StreamBuilder](#using-streambuilder)
- [Final Thoughts](#final-thoughts)

## Introduction to Streams

Streams in Dart are similar to observables in other programming languages, allowing you to react to a sequence of asynchronous events. They provide an efficient and readable way to handle asynchronous data in a reactive programming style.

## Creating a Stream

To create a stream in Dart, you need to import the "dart:async" package and use the `StreamController` class. Here's an example of how to create a basic stream:

```dart
import 'dart:async';

void main() {
  final StreamController<int> _streamController = StreamController<int>();
  
  // Add values to the stream
  _streamController.add(1);
  _streamController.add(2);
  _streamController.add(3);
  
  // Close the stream when done
  _streamController.close();
}
```

In the above example, we create a new `StreamController` and define the type of data it will emit (in this case, `int`). We can then use the `add` method to add data to the stream, and `close` to indicate that we have finished adding values.

## Adding Stream Listeners

To listen to a stream and react to its events, we can use the `listen` method. Here's an example of how to listen to a stream:

```dart
_streamController.stream.listen(
  (int value) {
    print('Received value: $value');
  },
  onError: (error) {
    print('Error occurred: $error');
  },
  onDone: () {
    print('Stream closed');
  }
);
```

In the above example, we call the `listen` method on the `stream` property of the `StreamController`. The `listen` method takes three optional parameters: `onData`, `onError`, and `onDone`. The `onData` callback is called each time a new value is added to the stream, `onError` is called when an error is encountered, and `onDone` is called when the stream is closed.

## Using StreamBuilder

The `StreamBuilder` widget in Flutter provides a concise way to listen to a stream and rebuild your UI when new data is received. Here's an example of how to use `StreamBuilder`:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  final StreamController<int> _streamController = StreamController<int>();

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Stream Example'),
        ),
        body: StreamBuilder<int>(
          stream: _streamController.stream,
          builder: (BuildContext context, AsyncSnapshot<int> snapshot) {
            if (snapshot.hasData) {
              return Text('Received value: ${snapshot.data}');
            } else if (snapshot.hasError) {
              return Text('Error occurred: ${snapshot.error}');
            } else {
              return CircularProgressIndicator();
            }
          },
        ),
      ),
    );
  }
}
```

In the above example, we create a simple Flutter app that displays the value received from the stream using the `Text` widget. We pass the stream to the `stream` parameter of the `StreamBuilder` widget, and use the `builder` function to define the UI that should be rebuilt whenever new data is received. The `snapshot` object contains the latest data received from the stream.

## Final Thoughts

Streams are a powerful feature in Flutter that allow you to handle asynchronous data in a reactive manner. By creating streams, adding listeners, and using the `StreamBuilder` widget, you can easily implement real-time functionality in your Flutter apps. Happy coding!

\#flutter \#dart