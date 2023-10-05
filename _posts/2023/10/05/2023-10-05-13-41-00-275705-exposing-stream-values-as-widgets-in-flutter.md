---
layout: post
title: "Exposing stream values as widgets in Flutter"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In Flutter, streams are a powerful tool for handling asynchronous data. They allow you to process and react to data as it becomes available. However, when it comes to displaying this data in the UI, you need to use widgets. In this blog post, we will explore how to expose stream values as widgets in Flutter.

## Table of Contents
- [Creating a Stream](#creating-a-stream)
- [Listening to Stream](#listening-to-stream)
- [Building Widgets](#building-widgets)
- [Updating UI](#updating-ui)
- [Conclusion](#conclusion)

## Creating a Stream

To expose stream values as widgets, you first need to create a stream. Streams can emit a sequence of events over time, and in the context of Flutter, these events represent the data you want to display in your UI.

Let's assume you have a stream that emits a list of `Product` objects. You can create this stream using the `StreamController` class provided by the `dart:async` library:

```dart
import 'dart:async';

class Product {
  final String name;
  final double price;

  Product(this.name, this.price);
}

class ProductStream {
  StreamController<List<Product>> _streamController = StreamController();

  Stream<List<Product>> get stream => _streamController.stream;

  void dispose() {
    _streamController.close();
  }
}
```

In the above code, we define a `Product` class representing our data model. Then, we create a `ProductStream` class with a `_streamController` to manage the stream. We expose the stream using the `get` keyword, allowing other classes to listen to it.

## Listening to Stream

Now that you have your stream, you need to listen to it and update the UI whenever new data is available. In Flutter, you can achieve this by using the `StreamBuilder` widget.

```dart
StreamBuilder<List<Product>>(
  stream: productStream.stream,
  builder: (context, snapshot) {
    if (snapshot.hasData) {
      final products = snapshot.data;
      // Render the widget with the stream data
      return ListView.builder(
        itemCount: products.length,
        itemBuilder: (context, index) {
          final product = products[index];
          return ListTile(
            title: Text(product.name),
            subtitle: Text('\$${product.price.toStringAsFixed(2)}'),
          );
        },
      );
    } else if (snapshot.hasError) {
      return Text('Error: ${snapshot.error}');
    } else {
      return CircularProgressIndicator();
    }
  },
)
```

In the above code, we wrap the UI code that needs to display stream values in the `builder` function of the `StreamBuilder` widget. The `snapshot` parameter gives us access to the latest state of the stream.

If the `snapshot` has data, we can extract it using `snapshot.data` and render our widget with the received data. If the `snapshot` has an error, we display an error message. If the stream is still loading, we show a circular progress indicator.

## Building Widgets

With the stream listener in place, you can now build your widgets and display the stream values in your UI. Use the `StreamBuilder` widget inside the build method of your widget tree to listen to the stream and update the UI accordingly.

```dart
class ProductListScreen extends StatelessWidget {
  final ProductStream productStream = ProductStream();

  @override
  void dispose() {
    productStream.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Product List'),
      ),
      body: StreamBuilder<List<Product>>(
        stream: productStream.stream,
        builder: (context, snapshot) {
          // ...
          // Use the snapshot data to build your widgets
          // ...
        },
      ),
    );
  }
}
```

In the above code, we define a `ProductListScreen` widget. Inside the `build` method, we create a `Scaffold` widget and wrap the UI that needs to display stream data inside the `StreamBuilder` widget.

## Updating UI

To update the UI when new data is available in the stream, you need to add values to the stream. This could be done from another part of your codebase or even from a network response. Whenever new values are added to the stream, the UI will automatically update.

```dart
productStream._streamController.add([Product('Shoes', 49.99)]);
```

In the above code, we use the `_streamController` instance to add a new list of `Product` objects to the stream. This will trigger the `builder` function of the `StreamBuilder` widget, updating the UI with the new data.

## Conclusion

Exposing stream values as widgets in Flutter is a straightforward process. By creating a stream, listening to it, and using the `StreamBuilder` widget, you can effectively display asynchronous data in your UI. Remember to handle errors and loading states appropriately to provide a smooth user experience.

By using streams and widgets together, you can create dynamic and responsive Flutter applications. Harness the power of streams to handle asynchronous data and update your UI in real-time.

#### #Flutter #Widgets