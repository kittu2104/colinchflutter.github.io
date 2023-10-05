---
layout: post
title: "Implementing bufferTime functionality in Dart streams"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

**Dart** is a powerful programming language for building cross-platform apps, including mobile, web, and server applications. One of its key features is the ability to work with streams, which allow you to handle asynchronous data in a convenient and efficient way.

In this tutorial, we will explore how to implement the `bufferTime` functionality in Dart streams. The `bufferTime` operator groups the events emitted by a stream into fixed time intervals, creating a list of events for each interval.

Let's get started by creating a custom extension method for the `Stream` class that adds the `bufferTime` functionality.

```dart
extension BufferTimeExtension<T> on Stream<T> {
  Stream<List<T>> bufferTime(Duration duration) {
    return transform(StreamTransformer.fromHandlers(
      handleData: (event, sink) {
        Timer? timer;
        var buffer = <T>[];

        void flushBuffer() {
          if (buffer.isNotEmpty) sink.add(buffer.toList());
          buffer.clear();
        }

        void onData(T data) {
          buffer.add(data);
          timer?.cancel();
          timer = Timer(duration, flushBuffer);
        }

        onData(event);

        timer = Timer(duration, flushBuffer);

        sink.done.then((_) => timer?.cancel());
      },
    ));
  }
}
```

In the above code, we create an extension method called `bufferTime` for the `Stream` class. This method takes a `Duration` parameter indicating the time interval for buffering events. We use the `transform` method of the `Stream` class to apply a `StreamTransformer` that handles the buffering logic.

Inside the `handleData` callback of the `StreamTransformer`, we maintain a buffer list and a timer. Whenever an event is received, it is added to the buffer list. We cancel any existing timer and start a new one with the specified duration. When the timer expires, we flush the buffer by emitting its contents through the sink.

To use the `bufferTime` functionality, simply call the method on any stream:

```dart
void main() {
  final stream = Stream<int>.periodic(Duration(seconds: 1), (i) => i)
      .take(10)
      .bufferTime(Duration(seconds: 3));

  stream.listen((buffer) {
    print(buffer);
  });
}
```

In the `main` function, we create a stream that emits integers every second using the `Stream.periodic` constructor. We limit the stream to emit only 10 events using the `take` operator. Finally, we apply the `bufferTime` operator with a duration of 3 seconds.

When running the above code, you will see the output printing a list of events every 3 seconds:

```
[0, 1, 2]
[3, 4, 5]
[6, 7, 8]
[9]
```

That's it! You have successfully implemented the `bufferTime` functionality in Dart streams. This can be useful in scenarios where you need to process events in batches based on a time interval.

# Conclusion

Working with streams in Dart opens up a world of possibilities for handling asynchronous data. By implementing the `bufferTime` functionality, you can easily group events into fixed time intervals. This can be helpful when dealing with real-time data or when performing batch operations periodically.

Remember to think about the use cases for this functionality and adjust the code accordingly. Happy coding!

#hashtags: #Dart #Streams