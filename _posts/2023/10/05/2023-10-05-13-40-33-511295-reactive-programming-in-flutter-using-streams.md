---
layout: post
title: "Reactive programming in Flutter using streams"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In Flutter, reactive programming is a powerful concept that allows you to build user interfaces that respond to changes in data. One way to implement reactive programming in Flutter is by using streams.

## What are Streams?

Streams are a way to handle asynchronous data in Dart. They provide a sequence of asynchronous events over time. You can think of a stream as a pipe that flows with data. It allows you to listen for new events and react to them accordingly.

## Implementing Streams in Flutter

To use streams in Flutter, you need to import the `dart:async` package. This package provides the necessary classes and methods for working with streams. Here's an example of how to create a simple stream in Flutter:

```dart
import 'dart:async';

void main() {
  final streamController = StreamController<int>();

  final streamSubscription = streamController.stream.listen((value) {
    print('Received: $value');
  });

  streamController.add(1);
  streamController.add(2);
  streamController.add(3);

  streamSubscription.cancel();
  streamController.close();
}
```

In the above example, we create a `StreamController` which is responsible for managing the stream. We then create a `StreamSubscription` by listening to the stream using the `listen` method. Whenever a new value is added to the stream using the `add` method, the listener function will be called.

## Using Reactive Programming in Flutter

To make use of reactive programming in Flutter, you can combine streams with widgets. The `StreamBuilder` widget provided by Flutter is a convenient way to handle streams and update the UI based on new data.

Here's an example of how to use the `StreamBuilder` widget:

```dart
import 'dart:async';

Stream<int> fetchData() async* {
  for (var i = 0; i < 5; i++) {
    await Future.delayed(Duration(seconds: 1));
    yield i;
  }
}

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Reactive Programming Demo',
      home: Scaffold(
        appBar: AppBar(title: Text('Reactive Programming Demo')),
        body: Center(
          child: StreamBuilder<int>(
            stream: fetchData(),
            builder: (context, snapshot) {
              if (snapshot.hasData) {
                return Text('Value: ${snapshot.data}');
              } else if (snapshot.hasError) {
                return Text('Error: ${snapshot.error}');
              } else {
                return CircularProgressIndicator();
              }
            },
          ),
        ),
      ),
    );
  }
}
```

In this example, the `fetchData` function returns a stream that emits values from 0 to 4 with a delay of 1 second between each value. The `StreamBuilder` listens to this stream and updates the UI accordingly.

The `snapshot` object provided by the stream builder allows you to access the current state of the stream. You can check if the stream has data using `snapshot.hasData`, if it has an error using `snapshot.hasError`, and display different UI components based on the stream state.

## Conclusion

Reactive programming with streams is a powerful way to handle asynchronous data in Flutter. By combining streams with widgets like `StreamBuilder`, you can create dynamic user interfaces that update in real-time as data changes. This allows you to build Flutter applications that are more responsive and maintain a smooth user experience.

#flutter #reactiveprogramming