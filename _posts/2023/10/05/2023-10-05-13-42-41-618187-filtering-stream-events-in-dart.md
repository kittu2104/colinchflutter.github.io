---
layout: post
title: "Filtering stream events in Dart"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In Dart, streams are a powerful asynchronous programming feature that allows you to handle a sequence of events over time. However, sometimes you may want to filter out specific events from a stream based on certain criteria. Thankfully, Dart provides several methods to simplify this task.

## Stream.where

The `where` method in the `Stream` class allows you to create a new stream that contains only the events that satisfy a given predicate. The predicate is a function that takes an event as its argument and returns a boolean value indicating whether the event should be included in the new stream.

Here's an example that demonstrates how to use `where` to filter out even numbers from a stream of integers:

```dart
import 'dart:async';

void main() {
  // Create a stream of integers from 1 to 10
  Stream<int> stream = Stream.fromIterable([1, 2, 3, 4, 5, 6, 7, 8, 9, 10]);

  // Filter out even numbers
  Stream<int> filteredStream = stream.where((event) => event % 2 != 0);

  // Print the filtered stream of odd numbers
  filteredStream.listen((event) => print(event));
}
```

In this example, the `where` method filters out any even numbers from the original stream and creates a new stream that only contains odd numbers. The `listen` method is then used to subscribe to the filtered stream and print each event.

## Stream.takeWhile

The `takeWhile` method in the `Stream` class allows you to create a new stream that contains events until a certain condition is no longer true. The condition is specified by a predicate function, similar to the `where` method.

Let's consider an example where we want to take events from a stream until we encounter a negative number:

```dart
import 'dart:async';

void main() {
  // Create a stream of integers
  Stream<int> stream = Stream.fromIterable([1, 2, 3, -4, -5, 6, 7, 8, 9, 10]);

  // Take events until a negative number is encountered
  Stream<int> takenStream = stream.takeWhile((event) => event >= 0);

  // Print the events until a negative number
  takenStream.listen((event) => print(event));
}
```

In this example, the `takeWhile` method creates a new stream that takes events from the original stream until it encounters a negative number. Once the condition becomes false, the stream stops emitting events, and the subscription is automatically canceled.

## Conclusion

Filtering stream events in Dart is made easy with the `where` and `takeWhile` methods provided by the `Stream` class. These methods allow you to create new streams that only contain the events that meet specific criteria. By combining these methods with other stream operations, you can efficiently process and manipulate asynchronous events in your Dart applications.

#dart #stream #filtering