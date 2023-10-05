---
layout: post
title: "Implementing takeUntil functionality in Dart streams"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

When working with Dart streams, it is often useful to be able to take items from a stream until a certain condition is met. This functionality is already available in many programming languages, but it is not natively supported in Dart. However, we can easily implement the `takeUntil` functionality ourselves using a combination of stream transformers and custom logic.

## Understanding the `takeUntil` Functionality

The `takeUntil` functionality allows us to listen to a stream until a specific condition occurs. Once the condition is met, the stream should stop emitting further items. This can be useful in scenarios where we want to listen to a stream until a specific event happens, or we want to limit the number of items we receive from a stream.

## Implementing the `takeUntil` Functionality

To implement the `takeUntil` functionality, we will make use of the `transform` method available on Dart streams. We will create a custom stream transformer that will listen to the source stream and pass items downstream until the specified condition is met. Once the condition is met, the transformer will stop listening to the source stream.

Here's an example implementation of a `takeUntil` transformer in Dart:

```dart
import 'dart:async';

extension TakeUntilExtension<T> on Stream<T> {
  Stream<T> takeUntil(bool Function(T) condition) {
    var controller = StreamController<T>();
    var subscription = this.listen(
      (event) {
        if (!condition(event)) {
          controller.add(event);
        } else {
          controller.close();
          subscription.cancel();
        }
      },
      onError: controller.addError,
      onDone: controller.close,
    );
    return controller.stream;
  }
}
```

In the above code, we define an extension on the `Stream<T>` datatype, which adds the `takeUntil` method. This method takes a `condition` function that evaluates whether an item from the stream should be taken or not. Inside the `takeUntil` method, we create a `StreamController` to emit the items downstream.

We then create a subscription to the source stream using the `listen` method. For each item received from the source stream, we check if the condition is met. If the condition is not met, we pass the item downstream using the `add` method. If the condition is met, we close the `StreamController` and cancel the subscription, effectively stopping the stream.

## Using the `takeUntil` Functionality

Once we have implemented the `takeUntil` functionality, using it is straightforward. We can simply chain it onto any Dart stream to control when items are taken from the stream.

Here's an example usage of the `takeUntil` functionality:

```dart
import 'dart:async';

void main() {
  var sourceStream = Stream.periodic(Duration(seconds: 1), (value) => value);

  var condition = (int value) => value == 5;

  var takenStream = sourceStream.takeUntil(condition);

  takenStream.listen((event) {
    print(event);
  });
}
```

In the above code, we define a source stream that emits a value every second using `Stream.periodic`. We then define a condition that should evaluate to true when we want to stop taking items from the source stream (in this case, when `value` reaches 5).

We use the `takeUntil` method on the `sourceStream` to create a new stream that only emits items until the condition is met. Finally, we listen to the `takenStream` and print each item received.

## Conclusion

Implementing the `takeUntil` functionality in Dart streams allows us to control when items are taken from a stream based on a specific condition. This can be useful in many scenarios where we need to listen to a stream until a certain event occurs. By creating a custom stream transformer and chaining it onto existing streams, we can easily add this functionality to our Dart applications.

#dart #streaming