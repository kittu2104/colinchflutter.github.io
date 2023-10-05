---
layout: post
title: "Implementing pairwiseAsObservable functionality in Flutter streams using Dart"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In this blog post, we will explore how to implement the `pairwiseAsObservable` function in Flutter streams using Dart programming language. This function allows us to generate a new stream that emits pairs of consecutive events from the original stream. This can be helpful in many scenarios where we need to process data in pairs or compare consecutive events.

## PairwiseAsObservable Function

The `pairwiseAsObservable` function takes a stream as input and returns a new stream that emits pairs of consecutive events. Here is the function signature:

```dart
Stream<List<T>> pairwiseAsObservable<T>(Stream<T> stream)
```

## Implementation

To implement the `pairwiseAsObservable` functionality, we need to create a new stream that listens to the original stream and emits pairs of consecutive events. Here is an example implementation in Dart:

```dart
import 'dart:async';

Stream<List<T>> pairwiseAsObservable<T>(Stream<T> stream) {
  StreamController<List<T>> controller;
  StreamSubscription<T> subscription;
  T previousEvent;

  controller = StreamController<List<T>>(
    onListen: () {
      subscription = stream.listen(
        (event) {
          if (previousEvent != null) {
            controller.add([previousEvent, event]);
          }
          previousEvent = event;
        },
        onError: controller.addError,
        onDone: controller.close,
        cancelOnError: true,
      );
    },
    onCancel: () => subscription.cancel(),
  );

  return controller.stream;
}
```

## Usage

Once we have implemented the `pairwiseAsObservable` function, we can use it with any stream to obtain pairs of consecutive events. Here is a simple example:

```dart
void main() {
  final stream = Stream<int>.fromIterable([1, 2, 3, 4, 5]);
  
  final pairwiseStream = pairwiseAsObservable(stream);
  
  pairwiseStream.listen((pair) {
    print(pair);
  });
}
```

Output:

```
[1, 2]
[2, 3]
[3, 4]
[4, 5]
```

In this example, we create a stream of integers `[1, 2, 3, 4, 5]` and then use the `pairwiseAsObservable` function to obtain pairs of consecutive events. We listen to the resulting stream and print each pair.

## Conclusion

In this blog post, we have learned how to implement the `pairwiseAsObservable` functionality in Flutter streams using Dart. This function allows us to generate a new stream that emits pairs of consecutive events from the original stream. By using this function, we can easily process data in pairs or compare consecutive events in our Flutter applications.

#flutter #dart