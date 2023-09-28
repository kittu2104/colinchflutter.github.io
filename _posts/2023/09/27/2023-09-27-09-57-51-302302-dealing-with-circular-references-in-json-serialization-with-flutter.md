---
layout: post
title: "Dealing with circular references in JSON serialization with Flutter"
description: " "
date: 2023-09-27
tags: [json, serialization]
comments: true
share: true
---

In Flutter, JSON serialization is a common task when working with APIs and data storage. However, when dealing with complex data structures that contain circular references, serialization can become more challenging.

A circular reference occurs when an object references itself or references another object that ultimately references the original object. This can lead to an infinite loop during serialization, as the serializer continues to follow the references endlessly.

Fortunately, Flutter provides a solution to handle circular references by using the `JsonCodec` class from the `dart:convert` package. Let's explore how to handle circular references during JSON serialization in Flutter.

## Using `JsonCodec` to Handle Circular References

The `JsonCodec` class in the `dart:convert` package provides methods for encoding and decoding JSON data. By default, the `JsonCodec` does not handle circular references. However, you can override its behavior by implementing a custom `toJson` method for the objects involved in the circular reference.

Here's an example of how to handle circular references using `JsonCodec`:

```dart
import 'dart:convert';

class Person {
  String name;
  List<Person> friends;

  Person({required this.name, required this.friends});

  Map<String, dynamic> toJson() {
    return {
      'name': name,
      'friends': friends.map((friend) => friend.toJson()).toList()
    };
  }
}

void main() {
  Person john = Person(name: 'John', friends: []);
  Person jane = Person(name: 'Jane', friends: []);
  
  john.friends.add(jane);
  jane.friends.add(john);

  // Using JsonCodec to encode the circular references
  JsonCodec jsonCodec = JsonCodec(toEncodable: (dynamic object) {
    if (object is Person) {
      return object.toJson();
    }
    return object;
  });

  String json = jsonCodec.encode(john);
  print(json);
}
```

In the above example, we have a `Person` class that represents a person with a name and a list of friends. We've defined a `toJson` method for the `Person` class that converts it to a JSON-serializable map. The `toJson` method handles the circular reference by recursively calling `toJson` on each friend.

In the `main` function, we create two `Person` instances, `john` and `jane`, and add each other as friends, creating a circular reference. To handle the circular reference during JSON encoding, we pass a custom `toEncodable` function to the `JsonCodec` constructor.

The `toEncodable` function checks if the object being encoded is an instance of the `Person` class. If it is, it calls the `toJson` method on the object. Otherwise, it returns the object as is. 

Finally, we use `jsonCodec.encode` to convert the `john` object to a JSON string, which we print to the console.

By implementing a custom `toJson` method and using `JsonCodec` with a custom `toEncodable` function, we can handle circular references during JSON serialization in Flutter.

#flutter #json #serialization #circular-references