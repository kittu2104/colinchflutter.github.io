---
layout: post
title: "Implementing interval functionality with a specific delay in Dart streams"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In Dart, streams are a powerful tool for handling asynchronous data streams. They allow you to receive and process data as they become available. However, there may be cases where you need to introduce a delay between each emission of data in a stream. This can be useful, for example, when you want to periodically update the UI with new data but also want to control the frequency at which updates occur.

In this article, we will explore how to implement an interval functionality with a specific delay in Dart streams using the `Stream` and `StreamController` classes.

## Table of Contents
1. [Creating the interval function](#creating-the-interval-function)
2. [Using the interval function](#using-the-interval-function)
3. [Conclusion](#conclusion)

## Creating the interval function

To create an interval function in Dart, we can define a stream controller that emits data at regular intervals. Here's an example implementation:

```dart
import 'dart:async';

Stream<int> interval(Duration duration) {
  StreamController<int> controller;
  Timer timer;
  int counter = 0;

  void tick(_) {
    counter++;
    controller.add(counter);
  }

  void startTimer() {
    timer = Timer.periodic(duration, tick);
  }

  void stopTimer() {
    timer?.cancel();
    timer = null;
  }

  void onData(void Function(int) handleData) {
    controller.stream.listen(handleData);
  }

  void dispose() {
    stopTimer();
    controller.close();
  }

  controller = StreamController<int>(
    onListen: startTimer,
    onCancel: stopTimer,
  );

  return controller.stream;
}
```

In this code, we define the `interval` function that takes a `Duration` parameter representing the delay between emissions. We then create a `StreamController` instance, which will be responsible for controlling the stream and emitting data.

Inside the `interval` function, we define a `tick` function that gets called at each interval. This function increments a `counter` variable and adds the counter value to the stream using the `controller.add` method.

Two helper functions, `startTimer` and `stopTimer`, are also defined to start and stop the timer respectively. The `Timer.periodic` function is used to create a recurring timer that calls the `tick` function at the specified intervals.

Finally, we define additional functions `onData` and `dispose` to listen for the stream data and clean up any resources respectively.

## Using the interval function

Now that we have our interval function defined, let's see how we can use it to create an interval stream:

```dart
void main() {
  final stream = interval(Duration(seconds: 1));

  final subscription = stream.listen((data) {
    print(data);
  });
  
  // Stop the stream after 5 seconds
  Timer(Duration(seconds: 5), () {
    subscription.cancel();
  });
}
```

In this example, we create a stream using the `interval` function with a delay of 1 second. We then listen to the stream using the `listen` method and print the emitted data.

To demonstrate how to stop the stream, we use a `Timer` to cancel the subscription after 5 seconds.

## Conclusion

By implementing an interval functionality with a specific delay in Dart streams, you can easily control the frequency at which data is emitted. This can be useful in scenarios such as updating the UI at regular intervals or periodically fetching data from an external source.

Dart streams provide a flexible way to handle asynchronous data, and by customizing the behavior of the stream using functionalities like interval, you can fit them into a wide range of use cases.