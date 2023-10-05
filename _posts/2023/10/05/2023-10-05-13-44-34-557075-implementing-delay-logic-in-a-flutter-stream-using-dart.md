---
layout: post
title: "Implementing delay logic in a Flutter stream using Dart"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In Flutter, streams are a powerful way to handle asynchronous data. They allow you to listen to and process continuous streams of data. However, there may be times when you need to introduce a delay between the data emitted by a stream. This can be useful in scenarios such as debouncing user input or throttling network requests. 

In this blog post, we will explore how to implement delay logic in a Flutter stream using Dart.

## Table of Contents
- [Understanding Streams in Flutter](#understanding-streams-in-flutter)
- [Introducing Delay in a Stream](#introducing-delay-in-a-stream)
- [Example: Debouncing User Input](#example-debouncing-user-input)
- [Conclusion](#conclusion)

## Understanding Streams in Flutter

Streams in Flutter are a way to handle asynchronous data. They can emit values over time and notify listeners whenever new data is available. 

To work with streams, you typically create a StreamController which acts as a source of data. You can then listen to this stream and perform operations on the emitted values.

## Introducing Delay in a Stream

To introduce a delay in a stream, we can use the `async` and `await` keywords provided by the Dart programming language. 

First, we need to convert the stream into a delayed stream. We can achieve this by using the `asyncMap` method provided by the Stream API. This method allows us to transform each event emitted by the stream into a delayed event.

```dart
Stream<dynamic> delayedStream(Stream<dynamic> input, Duration delay) async* {
  await for (final dynamic event in input) {
    await Future<void>.delayed(delay);
    yield event;
  }
}
```

The `delayedStream` function takes the original stream `input` and a `Duration` representing the delay. It then uses `async*` to create a generator function which iterates over the events emitted by the input stream. For each event, it introduces a delay using `Future<void>.delayed` method and yields the event.

Finally, we can use the delayed stream in our application code to introduce the desired delay.

## Example: Debouncing User Input

Let's consider an example where we want to debounce user input in a search bar. When the user types a character, we want to wait for a specified delay before performing the search operation.

```dart
final _searchController = StreamController<String>();

void search() {
  _searchController.stream
      .transform(delayedStream(const Duration(milliseconds: 500)))
      .listen((query) {
    // Perform search operation for the query
    print('Searching for $query');
  });
}

void onTextChanged(String text) {
  _searchController.add(text);
}
```

In this example, we create a stream controller `_searchController` to handle user input. We transform the stream using `delayedStream` and listen for search queries. When a query is received, we perform the search operation.

The `onTextChanged` method is invoked whenever the user types a character in the search bar. It adds the text to the stream, which triggers the debounce logic.

By adding a delay of 500 milliseconds in the `delayedStream`, we ensure that the search operation is not performed until the user has finished typing.

## Conclusion

Introducing delay logic in a Flutter stream can be useful in many scenarios, including debouncing user input and throttling network requests. By leveraging the `async` and `await` keywords in Dart, we can easily implement this functionality.

In this post, we provided an overview of how to introduce delay in a stream and demonstrated an example of debouncing user input. I hope you found this helpful in understanding how to implement delay logic in Flutter streams using Dart.

#flutter #dart