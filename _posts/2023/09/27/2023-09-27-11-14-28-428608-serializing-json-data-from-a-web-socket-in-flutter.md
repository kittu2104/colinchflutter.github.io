---
layout: post
title: "Serializing JSON data from a web socket in Flutter"
description: " "
date: 2023-09-27
tags: [Flutter, WebSocket]
comments: true
share: true
---

Flutter is a popular cross-platform framework for developing mobile applications. When working with real-time data from a web socket in Flutter, it is often necessary to serialize JSON data for further processing. In this blog post, we will explore how to deserialize JSON data received from a web socket and convert it into Flutter objects.

## Setting up the web socket connection

To begin, we need to establish a connection to the web socket server. Flutter provides the `web_socket_channel` package, which simplifies the process of working with web sockets. We can add this package to our `pubspec.yaml` file:

```yaml
dependencies:
  web_socket_channel: ^2.0.0
```

After adding the package, we need to import it in our Dart file:

```dart
import 'package:web_socket_channel/web_socket_channel.dart';
import 'package:web_socket_channel/io.dart';

final channel = IOWebSocketChannel.connect('wss://example.com/websocket');
```

In the above code, we create a web socket channel with the URL of the web socket server.

## Deserializing JSON data

To deserialize the incoming JSON data, we can create a class that represents the structure of the data. For example, if the JSON data contains a `name` and an `age` field, we can create a class like this:

```dart
class Person {
  final String name;
  final int age;

  Person({required this.name, required this.age});

  factory Person.fromJson(Map<String, dynamic> json) {
    return Person(
      name: json['name'],
      age: json['age'],
    );
  }
}
```

In the above code, we define a `Person` class with the required fields `name` and `age`. We also provide a factory method `fromJson` to deserialize the JSON data into a `Person` object.

To listen for incoming web socket messages, we can use the `channel.stream` property. We can then apply the `fromJson` factory method to convert the received JSON data into a `Person` object:

```dart
channel.stream.listen((message) {
  final data = jsonDecode(message);
  final person = Person.fromJson(data);
  
  // Do something with the deserialized person object
});
```

In the code above, we use the `jsonDecode` function from the `dart:convert` package to convert the incoming JSON message into a `Map`. We then pass the `Map` to the `fromJson` factory method of the `Person` class to deserialize it.

## Conclusion

In this blog post, we learned how to deserialize JSON data received from a web socket in Flutter. We saw how to set up a web socket connection using the `web_socket_channel` package and how to convert the incoming JSON data into Flutter objects using a class with a factory method. By following these steps, you can effectively handle real-time data from web sockets in your Flutter applications.

#Flutter #WebSocket #JSON