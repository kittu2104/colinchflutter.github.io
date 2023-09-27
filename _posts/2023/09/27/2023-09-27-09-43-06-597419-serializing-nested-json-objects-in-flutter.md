---
layout: post
title: "Serializing nested JSON objects in Flutter"
description: " "
date: 2023-09-27
tags: [jsonserialization]
comments: true
share: true
---

In Flutter, working with JSON data is quite common as it is widely used for data exchange between a client and server. Oftentimes, the JSON response may contain nested JSON objects, which can be challenging to handle. In this blog post, we will explore how to serialize nested JSON objects in Flutter using the `json_serializable` package.

To get started, make sure you have the `json_serializable` package added as a dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  json_annotation: <latest_version>
  json_serializable: <latest_version>
```

After adding the dependency, run `flutter pub get` to fetch the package.

## Step 1: Define the Model Classes

First, we need to define the model classes that represent the structure of the JSON data. Let's consider an example where we have a JSON response containing a user object with nested address information. Here's how the model classes could look like:

```dart
import 'package:json_annotation/json_annotation.dart';

part 'user.g.dart'; // This will be generated after step 2

@JsonSerializable()
class User {
  final String name;
  final int age;
  final Address address;

  User({this.name, this.age, this.address});

  factory User.fromJson(Map<String, dynamic> json) => _$UserFromJson(json);

  Map<String, dynamic> toJson() => _$UserToJson(this);
}

@JsonSerializable()
class Address {
  final String street;
  final String city;
  final String state;

  Address({this.street, this.city, this.state});

  factory Address.fromJson(Map<String, dynamic> json) => _$AddressFromJson(json);

  Map<String, dynamic> toJson() => _$AddressToJson(this);
}
```

You might have noticed some annotations (`@JsonSerializable`) and the `part` statement with the '.g.dart' file. These annotations and files are required for code generation, which we'll cover in the next step.

## Step 2: Generate Serializers

To automatically generate the serialization code, we need to run a build step that will create the necessary `.g.dart` files. Flutter recommends using the `build_runner` package to accomplish this. Ensure that you have `build_runner` added as a development dependency in your `pubspec.yaml`:

```yaml
dev_dependencies:
  build_runner: <latest_version>
```

Then, run the following command in your terminal:

```bash
flutter pub run build_runner build
```

This command scans the project for files annotated with `@JsonSerializable` and generates the necessary serialization code.

After running the above command, you will see that two new files are generated: `user.g.dart` and `address.g.dart`. These files contain the generated code for serializing and deserializing the JSON data.

## Step 3: Deserialize JSON

Now that we have the necessary serialization code generated, we can deserialize the JSON response. Assuming you have the JSON response stored in a variable called `jsonResponse`, you can convert it into a `User` object like this:

```dart
import 'dart:convert';

void main() {
  String jsonResponse = '{"name": "John Doe", "age": 25, "address": {"street": "123 ABC St", "city": "New York", "state": "NY"}}';
  
  User user = User.fromJson(json.decode(jsonResponse));
  
  print('Name: ${user.name}');
  print('Age: ${user.age}');
  print('Street: ${user.address.street}');
  print('City: ${user.address.city}');
  print('State: ${user.address.state}');
}
```

By decoding the JSON string using `json.decode`, we get a `Map<String, dynamic>`. Finally, calling `User.fromJson` on the decoded JSON map will deserialize the JSON into a `User` object.

## Step 4: Serialize to JSON

To serialize the `User` object back into a JSON string, you can call `toJson()` on the `User` object:

```dart
User user = User(name: 'John Doe', age: 25, address: Address(street: '123 ABC St', city: 'New York', state: 'NY'));

String jsonString = json.encode(user.toJson());

print('Serialized User: $jsonString');
```

The `toJson()` method converts the `User` object into a `Map<String, dynamic>`, which can then be encoded into a JSON string using `json.encode`.

That's it! You've successfully learned how to serialize and deserialize nested JSON objects in Flutter by leveraging the `json_serializable` package. This approach saves time and provides a structured way to handle complex JSON data in your Flutter applications.

#flutter #jsonserialization