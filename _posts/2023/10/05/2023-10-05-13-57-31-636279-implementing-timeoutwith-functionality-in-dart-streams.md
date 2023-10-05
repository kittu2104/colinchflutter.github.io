---
layout: post
title: "Implementing timeoutWith functionality in Dart streams"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In Dart, streams provide a convenient way to handle asynchronous data and events. There are several methods available for manipulating streams, but one commonly used method is `timeout`, which allows you to set a maximum duration for waiting on a stream event.

However, sometimes you may need more control over the timeout behavior. In such cases, you can implement the `timeoutWith` functionality to handle timeouts in a specific way. The `timeoutWith` function will wait for a certain amount of time, and if no event is received within that time, it will emit a default value or trigger a custom action.

Let's see how we can implement the `timeoutWith` functionality in Dart streams:

## The `timeoutWith` function

```dart
import 'dart:async';

extension TimeoutWithExtension<T> on Stream<T> {
  Stream<T> timeoutWith(Duration duration, {T Function()? onTimeout, Stream<T> Function()? fallbackStream}) async* {
    yield* this.transform(StreamTransformer<T, T>.fromHandlers(
      handleData: (event, sink) {
        sink.add(event);
      },
      handleDone: (sink) {
        sink.close();
      },
      handleError: (error, stackTrace, sink) {
        sink.addError(error, stackTrace);
      },
      handleCancel: (sink) {
        sink.close();
      },
    )).timeout(duration, onTimeout: () {
      if (fallbackStream != null) {
        return fallbackStream();
      } else if (onTimeout != null) {
        return Stream<T>.fromIterable([onTimeout()]);
      } else {
        throw TimeoutException("Stream timed out after $duration");
      }
    });
  }
}
```

## Usage

Once you have the `timeoutWith` function defined, you can use it with any stream to add the timeout functionality. Here's an example:

```dart
void main() {
  final stream = Stream<int>.fromIterable([1, 2, 3, 4, 5]);

  stream.timeoutWith(Duration(seconds: 2), onTimeout: () {
    return -1;
  }).listen((event) {
    print(event);
  }, onError: (error) {
    print(error);
  });
}
```

In the example above, we create a stream of integers and apply the `timeoutWith` function to it. We set the timeout duration to 2 seconds and specify a fallback value of -1 using the `onTimeout` callback. The `listen` method is used to handle the received events or errors.

If no event is received within the specified timeout duration, the fallback value of -1 will be emitted.

## Conclusion

Implementing the `timeoutWith` functionality in Dart streams gives you more control over handling timeouts in your asynchronous code. By customizing the fallback value or fallback stream, you can ensure that your code behaves as expected even when facing long wait times.

With the provided code example, you can start using the `timeoutWith` feature in your Dart projects to add robust timeout handling to your streams. Enjoy coding with Dart streams and don't forget to handle those timeouts effectively!

#dart #streams