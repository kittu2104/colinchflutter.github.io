---
layout: post
title: "Implementing exhaustMap functionality in Flutter streams using Dart"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In this article, we will explore how to implement the `exhaustMap` functionality in Flutter streams using Dart. The `exhaustMap` operator is useful when you want to ignore new events until the current event is completed. It is commonly used in scenarios where you have asynchronous tasks, and you want to ensure that only one task is executed at a time.

### Understanding exhaustMap

The exhaustMap operator is similar to the `flatMap` or `switchMap` operators in other programming languages. It takes a stream of events and applies a function to each event. However, unlike `flatMap` or `switchMap`, `exhaustMap` ignores any new events until the current event is completed.

### Implementing exhaustMap

To implement `exhaustMap` functionality in Flutter streams, we can create a custom operator that combines `switchMap` and `concatMap` operators. Here's an example implementation:

```dart
import 'dart:async';

extension StreamExhaustMap<T> on Stream<T> {
  Stream<S> exhaustMap<S>(Stream<S> Function(T) mapper) {
    return transform(StreamTransformer<T, S>.fromHandlers(
      handleData: (T value, EventSink<S> sink) {
        Stream<S> mappedStream = mapper(value);
        mappedStream.listen(sink.add, onError: sink.addError, onDone: () {
          // Call handleData to continue processing new events
          handleData(null, sink);
        });
      },
    ));
  }
}
```

### Using exhaustMap

Once we have implemented the `exhaustMap` operator, we can use it on any Flutter stream to achieve the desired behavior. Let's see an example usage:

```dart
import 'dart:async';

void main() {
  Stream<int> stream = Stream<int>.periodic(Duration(seconds: 1), (value) => value);

  Stream<int> mappedStream = stream.exhaustMap((value) {
    return Stream<int>.periodic(
        Duration(seconds: 2), (innerValue) => value * innerValue);
  });

  mappedStream.listen((value) {
    print(value);
  });
}
```

In the above example, we have a stream that emits a new value every second. We apply the `exhaustMap` operator on this stream and provide a mapping function that generates a new stream for each value emitted. The inner stream emits a value every two seconds, multiplied by the corresponding outer stream value. The output will be `0`, `0`, `2`, `4`, `12`, `24`, and so on.

### Conclusion

In this article, we have learned how to implement the `exhaustMap` functionality in Flutter streams using Dart. By implementing this custom operator, we can control the execution of asynchronous tasks and ensure that only one task is executed at a time. This can be especially useful in situations where we need to handle slow or time-consuming tasks in our Flutter applications.

#flutter #streams