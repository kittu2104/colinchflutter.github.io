---
layout: post
title: "Implementing toList functionality in Dart streams"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In Dart, streams are a powerful way to handle a sequence of asynchronous events. Sometimes, we may need to collect all the values emitted by a stream and convert them into a list. Dart provides a convenient `toList` method to achieve this. However, if you want to implement this functionality manually, you can do so using the `StreamSubscription` class and a callback function.

## Manual implementation of `toList` functionality

To manually implement the `toList` functionality in Dart streams, you can create a function that takes a stream as input and returns a future that completes with a list containing all the emitted values.

Here's an example implementation:

```dart
import 'dart:async';

Future<List<T>> toList<T>(Stream<T> stream) async {
  var list = <T>[];
  var completer = Completer<List<T>>();

  var subscription = stream.listen((value) {
    list.add(value);
  }, onError: (error) {
    completer.completeError(error);
  }, onDone: () {
    completer.complete(list);
  });

  await completer.future;
  await subscription.cancel();

  return list;
}
```

In this implementation, we create an empty list to store the emitted values. We also create a `Completer` to handle the completion of the future. The `StreamSubscription` listens to the stream and adds each emitted value to the list. If an error occurs, we complete the future with an error. Finally, when the stream ends, we complete the future with the list of values.

## Usage example

Let's see how we can use our custom `toList` function on a stream:

```dart
void main() async {
  var stream = Stream<int>.fromIterable([1, 2, 3, 4, 5]);
  var list = await toList(stream);

  print(list);
}
```

Running this Dart program will output:

```
[1, 2, 3, 4, 5]
```

As you can see, we successfully collected all the values emitted by the stream into a list.

## Conclusion

While Dart provides a built-in `toList` method on streams, manually implementing this functionality can give you more control and flexibility. By using the `StreamSubscription` class and a callback function, you can collect all the values emitted by a stream and convert them into a list. This can be useful in scenarios where you need to customize the list creation process or modify the emitted values before storing them.