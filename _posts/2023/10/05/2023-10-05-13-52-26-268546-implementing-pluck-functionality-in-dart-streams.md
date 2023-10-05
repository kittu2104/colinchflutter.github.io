---
layout: post
title: "Implementing pluck functionality in Dart streams"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

Dart streams provide a powerful way to work with asynchronous data. One common operation that is often needed when working with streams is extracting a specific property or value from each data event in the stream. This is similar to the `pluck` function found in some functional programming libraries.

In this blog post, we will explore how to implement the `pluck` functionality in Dart streams. We will start by understanding the problem statement and then move on to the implementation.

## Problem statement

When working with Dart streams, we often have a stream of objects where each object has multiple properties. However, in certain scenarios, we may only be interested in extracting a specific property from each object. For example, suppose we have a stream of employee objects, and we want to extract just the employee names from the stream.

## Solution

To implement the `pluck` functionality in Dart streams, we can define an extension method on the `Stream` class. This extension method will take a selector function as input, which will be responsible for extracting the desired property from each object.

```dart
extension StreamPluckExtension<T> on Stream<T> {
  Stream<R> pluck<R>(R Function(T) selector) {
    return map(selector);
  }
}
```

In the above code, we define an extension method `pluck` on the `Stream` class. It takes a generic type parameter `T` to represent the type of the objects in the stream. The extension method has another generic type parameter `R`, which represents the type of the property we want to extract.

The `pluck` method also takes a selector function as input, which is responsible for extracting the desired property from each object. The `selector` function takes an object of type `T` and returns the desired property of type `R`.

The implementation of the `pluck` method simply maps each object in the stream using the provided selector function. This returns a new stream of the extracted properties.

## Example usage

Let's see an example of how to use the `pluck` method on a stream of employee objects to extract the employee names.

```dart
class Employee {
  final String name;
  final int age;

  Employee(this.name, this.age);
}

void main() {
  final employees = [
    Employee('John Doe', 30),
    Employee('Jane Smith', 25),
    Employee('Mark Johnson', 35),
  ];

  final stream = Stream.fromIterable(employees);

  final namesStream = stream.pluck((employee) => employee.name);

  namesStream.listen((name) {
    print(name);
  });
}
```

In the above code, we define an `Employee` class with `name` and `age` properties. We create a list of `Employee` objects and convert it into a stream using `Stream.fromIterable()`. Then, we use the `pluck` method to extract the `name` property from each `Employee` object. Finally, we subscribe to the resulting stream and print the extracted names.

## Conclusion

Implementing the `pluck` functionality in Dart streams is a useful technique when working with streams of objects and needing to extract specific properties. By leveraging custom extension methods, we can create a more expressive and reusable codebase.