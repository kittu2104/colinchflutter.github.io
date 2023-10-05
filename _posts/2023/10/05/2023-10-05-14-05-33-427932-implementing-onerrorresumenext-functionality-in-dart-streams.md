---
layout: post
title: "Implementing onErrorResumeNext functionality in Dart streams"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

Dart streams are an essential feature in asynchronous programming, allowing us to handle a sequence of events over time. However, when working with streams, it's common to encounter errors that can disrupt the flow of data. One solution to gracefully handle errors is to implement the `onErrorResumeNext` functionality, which allows us to substitute the error with a fallback stream. In this blog post, we will explore how to implement `onErrorResumeNext` in Dart streams.

## Understanding onErrorResumeNext

The `onErrorResumeNext` functionality in Dart streams provides an elegant way to handle errors and continue the stream's flow with a fallback stream. When an error occurs in the source stream, instead of terminating the stream, we can provide a fallback stream that will continue emitting events.

## Implementing onErrorResumeNext

To implement `onErrorResumeNext` functionality in Dart streams, we can use a combination of stream.transform and StreamController. Let's see how we can achieve this:

```dart
import 'dart:async';

Stream<T> onErrorResumeNext<T>(Stream<T> source, Stream<T> fallbackStream) {
  final controller = StreamController<T>();

  source.listen(
    (event) {
      controller.add(event);
    },
    onError: (_) {
      fallbackStream.listen(
        (event) => controller.add(event),
        onError: (_) => controller.close(),
        onDone: () => controller.close(),
      );
    },
    onDone: () {
      controller.close();
    },
    cancelOnError: true,
  );

  return controller.stream;
}
```

In this code snippet, we define a generic function `onErrorResumeNext` that takes two parameters: the source stream and the fallback stream. We create a new `StreamController` to handle our transformed stream.

Inside the `listen` callback of the source stream, we forward the received events to the controller using `controller.add(event)`.

In case of an error, we subscribe to the fallback stream. The events emitted by the fallback stream are also forwarded to the controller.

Finally, we handle the `onDone` event by closing the controller.

## Example usage

Let's see an example usage of the `onErrorResumeNext` function:

```dart
void main() {
  final sourceStream = Stream<int>.fromIterable([1, 2, 3, 4, 5]);
  final fallbackStream = Stream<int>.fromIterable([10, 20, 30]);

  final transformedStream = onErrorResumeNext(sourceStream, fallbackStream);

  transformedStream.listen(
    (event) {
      print(event);
    },
    onError: (error) {
      print('An error occurred: $error');
    },
    onDone: () {
      print('Stream completed');
    },
  );
}
```

In this example, we have a source stream that emits integers from 1 to 5. We also have a fallback stream that emits integers 10, 20, and 30. We pass these two streams to `onErrorResumeNext` to create a transformed stream.

The transformed stream will emit events from the source stream until an error occurs, and then it will switch to emitting events from the fallback stream. In this case, the output will be:

```
1
2
3
4
5
Stream completed
```

## Conclusion

Implementing the `onErrorResumeNext` functionality in Dart streams provides a convenient way to handle errors and continue the stream's flow with a fallback stream. By using a combination of stream.transform and StreamController, we can gracefully handle errors and ensure that our streams keep emitting events.