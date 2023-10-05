---
layout: post
title: "How to listen to a stream in Flutter using Dart"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

Flutter is a powerful framework for building cross-platform applications. One common task in Flutter is listening to streams, which allows you to react to asynchronous events as they occur.

In this tutorial, we will learn how to listen to a stream in Flutter using the Dart programming language.

## Table of Contents
- [Creating a Stream](#creating-a-stream)
- [Listening to a Stream](#listening-to-a-stream)
- [Handling Stream Events](#handling-stream-events)
- [Canceling Stream Subscription](#canceling-stream-subscription)
- [Conclusion](#conclusion)

## Creating a Stream

Before we can listen to a stream, we need to create one. Streams in Dart are a sequence of asynchronous events, and can be created using the `Stream` class.

To create a simple stream, we can use the `Stream.fromIterable()` constructor. This constructor creates a stream from an existing iterable.

```dart
import 'dart:async';

void main() {
  // Create a stream from a list
  var stream = Stream.fromIterable([1, 2, 3, 4, 5]);

  // Use the stream
  stream.listen((data) {
    print(data);
  });
}
```

Here, we create a stream from a list of integers `[1, 2, 3, 4, 5]` using the `Stream.fromIterable()` constructor. We then listen to the stream using the `listen()` method and print each event as it occurs.

## Listening to a Stream

Once we have created a stream, we can use the `listen()` method to start listening to the stream and react to events.

```dart
void main() {
  var stream = Stream.fromIterable([1, 2, 3, 4, 5]);

  stream.listen((data) {
    print(data);
  });
}
```

In the above example, we create a stream and listen to it. The callback function `print(data)` is called for each event in the stream, printing the value to the console.

## Handling Stream Events

Streams in Dart can have different types of events. To handle different types of events, we can use the `listen()` method with optional named parameters.

For example, we can handle the `onData` event when new data is available, the `onError` event when an error occurs, and the `onDone` event when the stream is finished.

```dart
void main() {
  var stream = Stream.fromIterable([1, 2, 3, 4, 5]);

  stream.listen(
    (data) {
      print('Data: $data');
    },
    onError: (error) {
      print('Error: $error');
    },
    onDone: () {
      print('Stream Done');
    },
  );
}
```

In the example above, we handle the `onData` event by printing `Data: $data` for each event in the stream. We also handle the `onError` event by printing the error message, and the `onDone` event by printing `Stream Done` when the stream is finished.

## Canceling Stream Subscription

To stop listening to a stream, we can cancel the stream subscription returned by the `listen()` method. This can be done by calling the `cancel()` method on the subscription.

```dart
void main() {
  var stream = Stream.fromIterable([1, 2, 3, 4, 5]);

  var subscription = stream.listen((data) {
    print(data);
  });

  // Cancel the subscription after 3 seconds
  Future.delayed(Duration(seconds: 3), () {
    subscription.cancel();
    print('Canceled subscription');
  });
}
```

In the example above, we create a stream and listen to it. After a delay of 3 seconds using `Future.delayed()`, we cancel the subscription using `subscription.cancel()`.

## Conclusion

Listening to a stream in Flutter using Dart is a powerful way to react to asynchronous events. By creating a stream, listening to events, and handling different types of events, we can build responsive and reactive applications.

Remember to cancel stream subscriptions when they are no longer needed to avoid unnecessary resource usage.

I hope this article has helped you understand how to listen to a stream in Flutter. Happy coding!

#flutter #dart