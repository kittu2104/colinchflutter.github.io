---
layout: post
title: "Serializing enum values in JSON with Flutter"
description: " "
date: 2023-09-27
tags: [json, serialization]
comments: true
share: true
---

Enums are a convenient way to represent fixed sets of values in programming languages. In Flutter, enums can be used to define a set of possible values for a variable. 

When working with APIs that use JSON as the data format, you may need to serialize and deserialize enum values to and from JSON. In this blog post, we will explore how to serialize enum values to JSON using the `dart:convert` package in Flutter.

## Serializing Enum Values to JSON

To serialize enum values to JSON, you can take advantage of the `toJson()` method of the enum class. 

Here's an example of how you can serialize an enum value to JSON:

```dart
enum Color { red, green, blue }

void main() {
  Color color = Color.blue;
  
  String jsonString = color.toString().split('.').last; // Get the enum value as a string
  print(jsonString); // Output: blue
}
```

In the code above, we define an enum called `Color` with three possible values: `red`, `green`, and `blue`. We then create an instance of the `Color` enum with the `Color.blue` value. By calling `toString()` on the enum value, we get a string representation of the enum value with the format `Color.blue`. We use the `split()` method to extract the last part of the string, which corresponds to the enum value itself and convert it to JSON.

## Deserializing Enum Values from JSON

To deserialize enum values from JSON, you can use the `Color.values` property to get a list of all the possible enum values. You can then look for the enum value that matches the JSON string and use it in your application.

Here's an example of how you can deserialize an enum value from JSON:

```dart
enum Color { red, green, blue }

void main() {
  String jsonString = 'blue';
  
  Color color = Color.values.firstWhere((c) => c.toString().split('.').last == jsonString);
  print(color); // Output: Color.blue
}
```

In the code above, we have a JSON string `blue` and we want to deserialize it back into an enum value. We use the `Color.values` property to get a list of all the possible enum values, and then use the `firstWhere()` method to find the enum value that matches the JSON string. 

Note that if the JSON string does not match any of the enum values, an exception will be thrown. You can handle this by providing a default value or using a try-catch block to handle the exception.

## Conclusion

Serializing and deserializing enum values to and from JSON is a common requirement when working with APIs. In this blog post, we explored how to serialize enum values to JSON using the `toJson()` method, and how to deserialize enum values from JSON using `Color.values` and `firstWhere()`.

By implementing these techniques, you can easily work with enum values while communicating with APIs that use JSON as the data format in your Flutter applications.

#flutter #json #serialization