---
layout: post
title: "Implementing publishValue functionality in Flutter streams using Dart"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In Flutter, streams are a way to handle asynchronous data flow. They allow you to receive and process data as it becomes available. However, one limitation of streams in Flutter is that once you listen to a stream, you will only receive data from that point forward. There is no built-in functionality to get the last emitted value of a stream.

In many cases, it's useful to have the ability to get the last value emitted by a stream even after subscribing to it. This is especially helpful when you want to update the UI with the current state of the stream as soon as you start listening to it.

To implement this behavior, you can create a custom class that extends `Stream` and adds a `publishValue` method. Here's an example implementation in Dart:

```dart
import 'dart:async';

class PublishValueStream<T> extends Stream<T> {
  StreamController<T> _controller;
  T _lastValue;

  PublishValueStream() {
    _controller = StreamController<T>.broadcast(
      onListen: () {
        if (_lastValue != null) {
          _controller.add(_lastValue);
        }
      },
    );
  }

  void publishValue(T value) {
    _lastValue = value;
    _controller.add(value);
  }

  @override
  StreamSubscription<T> listen(
    void Function(T event) onData, {
    Function onError,
    void Function() onDone,
    bool cancelOnError,
  }) {
    return _controller.stream.listen(
      onData,
      onError: onError,
      onDone: onDone,
      cancelOnError: cancelOnError,
    );
  }
}
```

In this implementation, we create a `StreamController` with the `broadcast` flag set to `true`. This allows multiple subscribers to listen to the stream. We override the `onListen` callback to immediately emit the last value to any new subscribers.

The `publishValue` method updates the last value and adds it to the stream. Subscribers will receive the last value immediately when they start listening.

To use the `PublishValueStream`, you can create an instance of it and subscribe to it using the `listen` method:

```dart
void main() {
  final stream = PublishValueStream<int>();

  stream.publishValue(10);

  stream.listen((value) {
    print('Received value: $value');
  });

  stream.publishValue(20);
}
```

In this example, we publish two values, 10 and 20. The subscriber will receive the last value, 20, as soon as it starts listening.

By implementing the `publishValue` functionality, you can have more control over your streams in Flutter, allowing you to handle the current state of the data as well as new updates. This can be particularly useful for updating UI elements or maintaining the application's state.

#flutter #dart