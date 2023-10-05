---
layout: post
title: "Implementing skipLast functionality in Dart streams"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

When working with streams in Dart, you may often come across scenarios where you need to skip the last few elements emitted by the stream before processing the remaining ones. While there is no built-in `skipLast` functionality in Dart streams, you can easily implement it yourself using the existing stream operators.

In this blog post, we will guide you on how to implement the `skipLast` functionality in Dart streams using a custom stream transformer.

## Table of Contents
- [Overview](#overview)
- [Implementing the skipLast Transformer](#implementing-the-skiplast-transformer)
- [Usage](#usage)
- [Conclusion](#conclusion)

## Overview

The skipLast functionality allows you to skip a specified number of elements at the end of a stream. For example, if you have a stream that emits values [1, 2, 3, 4, 5] and you want to skip the last 2 elements, the resulting stream would emit [1, 2, 3].

## Implementing the skipLast Transformer

To implement the skipLast functionality, we will create a custom stream transformer. A stream transformer allows us to transform the original stream into a new stream by applying a set of operations.

Here's an example implementation of the skipLast transformer:

```dart
import 'dart:async';

class SkipLastStreamTransformer<T> extends StreamTransformerBase<T, T> {
  final int count;

  SkipLastStreamTransformer(this.count);

  @override
  Stream<T> bind(Stream<T> stream) {
    var controller = StreamController<T>();

    var buffer = <T>[];

    // Listen to the original stream and buffer the elements
    var subscription = stream.listen(
      (value) => buffer.length < count ? buffer.add(value) : buffer.addLast(value),
      onError: controller.addError,
      onDone: () {
        // Emit the buffered elements
        for (var element in buffer) {
          controller.add(element);
        }
        controller.close();
      },
      cancelOnError: true,
    );

    return controller.stream;
  }
}
```

In the above implementation, we create a custom stream transformer class `SkipLastStreamTransformer` that takes the number of elements to skip as a parameter. We use a `StreamController` to create a new stream and buffer the elements until we reach the desired count. Once the original stream completes, we emit the buffered elements in the new stream.

## Usage

To use the skipLast functionality in your Dart code, follow these steps:

1. Import the necessary libraries:
   ```dart
   import 'dart:async';
   ```

2. Create a stream and apply the skipLast transformer:
   ```dart
   void main() {
      var stream = Stream.fromIterable([1, 2, 3, 4, 5])
        .transform(SkipLastStreamTransformer(2));
   
      stream.listen((value) => print(value));
   }
   ```

   The above code skips the last 2 elements of the stream and prints the remaining elements [1, 2, 3].

## Conclusion

Implementing the skipLast functionality in Dart streams allows you to skip a certain number of elements at the end of a stream. By creating a custom stream transformer, you can easily add this capability to your streams. We hope this blog post has been helpful in guiding you through the implementation process. Happy coding!

**#Dart #StreamTransformers**