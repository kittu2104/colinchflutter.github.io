---
layout: post
title: "Serializing objects with inheritance in JSON using Flutter"
description: " "
date: 2023-09-27
tags: [JSON]
comments: true
share: true
---

In Flutter, serializing objects into JSON format allows us to conveniently transport and store data. When dealing with inheritance, we may have a base class with multiple subclasses, each having its own set of properties. In this blog post, we will explore how to correctly serialize objects with inheritance in JSON using Flutter.

## Setup
Before we begin, make sure you have a Flutter development environment set up on your machine.

## Creating the Base Class
Let's start by creating a base class with some common properties that will be inherited by the subclasses. In this example, let's create a class called `Animal` with two properties: `name` and `age`.


```dart
class Animal {
  final String name;
  final int age;

  Animal({required this.name, required this.age});

  Map<String, dynamic> toJson() {
    return {
      'name': name,
      'age': age,
    };
  }
}
```

## Creating Subclasses
Now, let's create two subclasses that inherit from the `Animal` class: `Cat` and `Dog`. Each subclass will add its own set of properties and override the `toJson` method to include the subclass-specific properties.


### Cat subclass

```dart
class Cat extends Animal {
  final String catBreed;
  final String color;

  Cat({required String name, required int age, required this.catBreed, required this.color})
      : super(name: name, age: age);

  @override
  Map<String, dynamic> toJson() {
    var json = super.toJson();
    json['catBreed'] = catBreed;
    json['color'] = color;
    return json;
  }
}
```

### Dog subclass

```dart
class Dog extends Animal {
  final String dogBreed;
  final bool isFriendly;

  Dog({required String name, required int age, required this.dogBreed, required this.isFriendly})
      : super(name: name, age: age);

  @override
  Map<String, dynamic> toJson() {
    var json = super.toJson();
    json['dogBreed'] = dogBreed;
    json['isFriendly'] = isFriendly;
    return json;
  }
}
```

## Serialization
To convert an instance of a subclass into JSON, we can simply call the `toJson` method on the object. Here's an example:

```dart
void main() {
  var cat = Cat(name: 'Whiskers', age: 2, catBreed: 'Siamese', color: 'Brown');
  var catJson = cat.toJson();
  print(catJson);
  
  var dog = Dog(name: 'Buddy', age: 4, dogBreed: 'Golden Retriever', isFriendly: true);
  var dogJson = dog.toJson();
  print(dogJson);
}
```

The output will be:

```json
{
  "name": "Whiskers",
  "age": 2,
  "catBreed": "Siamese",
  "color": "Brown"
}

{
  "name": "Buddy",
  "age": 4,
  "dogBreed": "Golden Retriever",
  "isFriendly": true
}
```

As you can see, the `toJson` method correctly serializes the object and includes the subclass-specific properties.

## Conclusion
Serializing objects with inheritance in JSON allows us to store and transport complex data structures conveniently. By implementing the `toJson` method in the base class and overriding it in the subclasses, we can easily convert objects into JSON format in Flutter.

Don't forget to check out the official [Flutter documentation](https://flutter.dev/docs) for more information on serialization and other useful features. #Flutter #JSON #Serialization #Inheritance