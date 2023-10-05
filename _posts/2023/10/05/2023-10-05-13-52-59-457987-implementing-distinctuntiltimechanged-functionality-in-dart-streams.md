---
layout: post
title: "Implementing distinctUntilTimeChanged functionality in Dart streams"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

Dart is a programming language developed by Google that is widely used for building mobile, web, and server-side applications. One of the powerful features of Dart is its support for streams, which allow you to work with asynchronous data in a more concise and expressive way.

In this blog post, we will explore how to implement the `distinctUntilTimeChanged` functionality in Dart streams. This functionality ensures that a value emitted by a stream is not repeated within a certain time period, providing more control over the data flow.

## Understanding `distinctUntilTimeChanged`

The `distinctUntilTimeChanged` functionality is useful when you want to ensure that only unique values are emitted by a stream, allowing a certain time window for the values to change. This is particularly helpful in scenarios where you receive rapid updates from a stream but only need to process new values after a certain period of time.

## Implementing `distinctUntilTimeChanged`

To implement the `distinctUntilTimeChanged` functionality in Dart streams, we can leverage existing stream operators and a Timer. Here's an example implementation:

```dart
import 'dart:async';

Stream<T> distinctUntilTimeChanged<T>(Stream<T> sourceStream, Duration duration) {
  StreamController<T> controller;
  T previousValue;
  Timer timer;

  void onData(T value) {
    if (value != previousValue) {
      timer?.cancel();
      timer = Timer(duration, () {
        controller.add(value);
      });
    }

    previousValue = value;
  }

  void onDone() {
    controller.close();
  }

  controller = StreamController<T>(
    onListen: () {
      sourceStream.listen(onData, onDone: onDone);
    },
  );

  return controller.stream;
}
```

In this implementation, we create a new stream controller and store the previous value and a timer as part of the functionality. The `onData` function is called for each value emitted by the source stream. If the value is different from the previous value, we cancel any existing timer and start a new timer. When the timer expires, we emit the current value. This ensures that only distinct values are emitted within the specified duration.

## Using the `distinctUntilTimeChanged` operator

Now that we have implemented the `distinctUntilTimeChanged` functionality, let's see how we can use it with streams. Suppose we have a stream that emits temperature values, and we want to process only the temperatures that change within a 5 second interval.

```dart
void main() {
  final temperatureStream = Stream.periodic(Duration(seconds: 1), (i) => i % 3 + 20)
      .take(10); // Simulated temperature stream

  final distinctTemperaturesStream =
      distinctUntilTimeChanged(temperatureStream, Duration(seconds: 5));

  distinctTemperaturesStream.listen((temperature) {
    print('New temperature: $temperature');
  });
}
```

In this example, we create a simulated temperature stream that emits a value every second, starting from 20 and incrementing in a cyclic manner. We use `distinctUntilTimeChanged` and specify a 5-second duration to only receive temperatures that change within that timeframe. The resulting stream is then listened to, and whenever a distinct temperature is emitted, it is printed to the console.

## Conclusion

By implementing the `distinctUntilTimeChanged` functionality in Dart streams, we can effectively filter out duplicate values and only process data that changes within a specific time window. This can be useful in scenarios where you need to handle frequent updates but only act upon new or changed values. Dart's stream functionality provides a powerful toolset for working with asynchronous data in a clean and expressive way.

Remember to [follow us on Twitter](https://twitter.com/mytechblog) for more tech-related content!

#dart #streams #distinctUntilTimeChanged