---
layout: post
title: "Implementing distinctUntilKeyChanged functionality in Flutter streams using Dart"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

When working with streams in Flutter, you may come across a scenario where you only want to receive values from a stream if a specific key in the emitted objects has changed. This behavior is similar to the `distinctUntilChanged` operator in RxJava or the `distinctUntilKeyChanged` operator in RxJS.

In Dart, you can achieve this functionality by creating a custom stream transformer. A stream transformer is an object that transforms a stream into another stream by applying a series of operations.

Here's an example implementation of the `distinctUntilKeyChanged` functionality as a custom stream transformer:

```dart
import 'dart:async';

class DistinctUntilKeyChangedStreamTransformer<T> extends StreamTransformerBase<List<T>, T> {
  final T Function(List<T>) keySelector;
  
  DistinctUntilKeyChangedStreamTransformer(this.keySelector);
  
  @override
  Stream<T> bind(Stream<List<T>> stream) {
    return stream.transform(StreamTransformer.fromHandlers(handleData: (List<T> data, EventSink<T> sink) {
      T currentKey;
      
      for (T item in data) {
        final key = keySelector(item);
        
        if (currentKey != key) {
          currentKey = key;
          sink.add(item);
        }
      }
    }));
  }
}
```

In the `DistinctUntilKeyChangedStreamTransformer` class, we define a `keySelector` function that receives a list of items and returns the key based on which we want to filter the stream. 

Inside the `bind` method, we 
- Transform the input stream using the `transform` method with a `StreamTransformer.fromHandlers` transformer. 
- Set up a `handleData` callback to process each emitted data event.
- Keep track of the current key using a `currentKey` variable. 
- Check if the current key is different from the key of the current item. If they are different, add the item to the output stream using the `sink.add` method. 

To use this custom stream transformer, you can simply chain it with your existing stream:

```dart
final stream = Stream.fromIterable([
  {'id': 1, 'name': 'John'},
  {'id': 2, 'name': 'Jane'},
  {'id': 2, 'name': 'John'},
  {'id': 3, 'name': 'Jane'},
]).transform(DistinctUntilKeyChangedStreamTransformer((item) => item['id']));

stream.listen((item) {
  print(item);
});
```

In this example, we have a stream of maps representing users, and we want to filter the stream based on the 'id' key. With the help of the `DistinctUntilKeyChangedStreamTransformer`, only the first occurrence of each unique 'id' will be emitted by the resulting stream.

With this implementation, you can easily filter and process the stream based on changes in a specific key using Dart and Flutter.

#flutter #dart