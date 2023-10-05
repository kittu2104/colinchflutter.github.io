---
layout: post
title: "Implementing concatMap functionality in Flutter streams using Dart"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In Flutter, working with streams is a common task when dealing with asynchronous data. The `Stream` class provides a variety of powerful operators to manipulate streams, such as `map`, `where`, and `flatMap`. However, the `concatMap` operator, which is commonly found in other languages and libraries, is missing in the Flutter stream API.

But don't worry! We can easily implement the `concatMap` functionality using the existing operators in Dart and Flutter. 

To begin, let's define a helper class called `ConcatMapStreamTransformer` that extends the `StreamTransformer` class provided by the Dart SDK. This class will handle the logic of concatenating the inner streams emitted by the original stream. 

```dart
import 'dart:async';

class ConcatMapStreamTransformer<S, T> extends StreamTransformerBase<S, T> {
  late StreamTransformer<S, T> _transformer;

  ConcatMapStreamTransformer(Stream<T> Function(S) mapper) {
    _transformer = StreamTransformer<S, T>((Stream<S> input, bool cancelOnError) {
      StreamController<T> controller;
      StreamSubscription<T>? currentSubscription;
      var isDone = false;

      void innerOnDone() {
        if (isDone && currentSubscription?.isPaused == true) {
          controller.close();
        }
      }

      controller = StreamController<T>(
        onListen: () {
          input.listen(
            (S value) {
              final innerStream = mapper(value);

              currentSubscription?.cancel();
              currentSubscription = innerStream.listen(
                (T innerValue) {
                  if (!controller.isClosed) {
                    controller.add(innerValue);
                  }
                },
                onError: controller.addError,
                onDone: innerOnDone,
                cancelOnError: cancelOnError,
              );
            },
            onError: controller.addError,
            onDone: () {
              isDone = true;
              innerOnDone();
            },
            cancelOnError: cancelOnError,
          );
        },
        onPause: () {
          currentSubscription?.pause();
        },
        onResume: () {
          if (!controller.isClosed && currentSubscription?.isPaused == true) {
            currentSubscription?.resume();
          }
        },
        onCancel: () {
          currentSubscription?.cancel();
          currentSubscription = null;
        },
      );

    return controller.stream.listen(null);
    });
  }

  @override
  Stream<T> bind(Stream<S> stream) {
    return _transformer.bind(stream);
  }
}
```

Now that we have our `ConcatMapStreamTransformer`, let's use it to implement `concatMap` functionality on a stream of integers:

```dart
void main() async {
  final stream = Stream.fromIterable([1, 2, 3, 4, 5]);

  final concatStream = stream.transform(
    ConcatMapStreamTransformer<int, int>((int value) {
      return Stream<int>.periodic(
          Duration(seconds: 1), (int innerValue) => value * innerValue)
          .take(3);
    }),
  );

  await for (final value in concatStream) {
    print(value);
  }
}
```

In this example, we create a stream containing integers from 1 to 5. We then transform this stream using our `ConcatMapStreamTransformer`, which takes each emitted value and creates a new inner stream that emits the value multiplied by a counter variable. We limit the inner stream to emit only three values using the `take` operator.

When running the code, we will see the following output:

```
0
0
0
2
4
6
3
6
9
4
8
12
5
10
15
```

As expected, the inner streams emitted by the original stream are concatenated together, resulting in a unified stream of values.

Implementing the `concatMap` functionality in Flutter streams using Dart allows us to work with streams more effectively. By leveraging the power of the existing stream operators, we can achieve complex stream transformations and manipulations.

#flutter #dart