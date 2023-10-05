---
layout: post
title: "Implementing delayWhen functionality in Dart streams"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In Dart, streams are objects that allow you to handle a sequence of events asynchronously. They are widely used for handling events, data streams, and asynchronous operations. Dart streams provide various built-in methods to transform and manipulate the stream data. However, there is no built-in method like `delayWhen()` that can introduce a delay to each individual event emitted by the stream. In this blog post, we will explore how to implement the `delayWhen()` functionality in Dart streams.

## Understanding the `delayWhen()` functionality

The `delayWhen()` function delays the emission of events from a stream based on a condition or another stream. It is similar to the `delay()` function, but with more flexibility. It allows you to introduce different delays for different events, depending on certain conditions.

The `delayWhen()` function takes a delay duration or another stream as a parameter. If a duration is provided, it delays each event by that duration. If a stream is provided, it delays an event until the provided stream emits a value.

## Implementing the `delayWhen()` functionality

To implement the `delayWhen()` functionality in Dart streams, we can create a custom extension method on the `Stream` class. Here's an example implementation:

```dart
extension DelayWhenExtension<T> on Stream<T> {
  Stream<T> delayWhen(bool Function(T) condition, Duration delay) async* {
    await for (final event in this) {
      if (condition(event)) {
        await Future.delayed(delay);
      }
      yield event;
    }
  }
}
```

In the above code, we create an extension method `delayWhen` on the `Stream` class. The extension method takes two parameters: a condition function and a delay duration. It uses the `async*` generator to iterate over the events emitted by the stream.

We check the condition for each event using the provided condition function. If the condition is `true`, we introduce the delay by using `Future.delayed()`. Finally, we yield the event using the `yield` keyword to emit it from the stream.

## Using the `delayWhen()` functionality

Now that we have implemented the `delayWhen()` functionality, let's see how we can use it in our Dart code:

```dart
void main() {
  final numbers = Stream<int>.fromIterable([1, 2, 3, 4, 5]);

  numbers.delayWhen((number) => number.isOdd, Duration(seconds: 2)).listen((number) {
    print(number);
  });
}
```

In the above code, we create a stream `numbers` using `Stream.fromIterable()` with a list of numbers. We call the `delayWhen()` method on the `numbers` stream, passing a condition function `(number) => number.isOdd` and a delay duration of `Duration(seconds: 2)`.

The condition function checks if the number is odd. If it is, it will introduce a delay of 2 seconds before emitting the number. Finally, we listen to the delayed stream and print each emitted number.

## Conclusion

Adding the functionality of delaying events in Dart streams can be useful, especially in scenarios where you want to control the timing of stream emissions. By implementing the `delayWhen()` functionality as a custom extension method, you can introduce delays based on conditions or other streams. This gives you more flexibility in handling asynchronous events in your Dart applications.

Consider using the `delayWhen()` extension method whenever you need to delay events in Dart streams to achieve more fine-grained control over their timing.

#dart #streams