---
layout: post
title: "Transforming JSON data during serialization with Flutter"
description: " "
date: 2023-09-27
tags: [JSON, serialization]
comments: true
share: true
---

Serialization is an essential part of working with JSON data in any programming language, including Flutter. It allows us to convert JSON data into Dart objects and vice versa. However, sometimes we need to perform additional transformations on the JSON data during the serialization process.

In this blog post, we will explore how to transform JSON data during serialization using the built_value package in Flutter. The built_value package provides a powerful way to define immutable value types and serialize them to and from JSON.

## Installation

To get started, we need to add the built_value package as a dependency in our `pubspec.yaml` file:

```yaml
dependencies:
  built_value: ^7.0.0
  built_value_generator: ^7.0.0
  built_collection: ^5.0.0
```

After adding the dependencies, run `flutter pub get` to fetch them.

## Defining the model

Let's say we have a JSON object representing a user with the following structure:

```json
{
  "id": 1,
  "name": "John Doe",
  "email": "john.doe@example.com"
}
```

To transform this JSON data, we need to define a model class and annotate it with the necessary annotations from the built_value package.

```dart
import 'package:built_value/built_value.dart';
import 'package:built_value/serializer.dart';

part 'user_model.g.dart';

abstract class UserModel implements Built<UserModel, UserModelBuilder> {
  int get id;
  String get name;

  @BuiltValueField(wireName: 'email')
  String get emailAddress;

  UserModel._();

  factory UserModel([void Function(UserModelBuilder) updates]) = _$UserModel;

  static Serializer<UserModel> get serializer => _$userModelSerializer;
}
```

In the above code, we define a `UserModel` class with getters for `id`, `name`, and `emailAddress`. The `@BuiltValueField` annotation is used to specify the custom JSON key, `email`, corresponding to the `emailAddress` property.

## Generating serialization code

To generate the serialization code, run the following command:

```bash
flutter packages pub run build_runner build
```

This generates the necessary code for JSON serialization in the `user_model.g.dart` file.

## Transforming JSON data

To transform the JSON data during serialization, we need to create a custom serializer for the `UserModel` class. Let's say we want to transform the `emailAddress` property to lowercase before serializing it.

```dart
import 'package:built_value/serializer.dart';
import 'package:built_value/standard_json_plugin.dart';

class LowercaseEmailSerializerPlugin implements SerializerPlugin {
  @override
  Object? beforeDeserialize(Object serialized, FullType specifiedType) {
    return serialized;
  }

  @override
  Object? afterDeserialize(Object deserialized, FullType specifiedType) {
    return deserialized;
  }

  @override
  Object? beforeSerialize(Object object, FullType specifiedType) {
    if (specifiedType.root == UserModel) {
      final userModel = object as UserModel;
      return userModel.rebuild((b) => b..emailAddress = userModel.emailAddress.toLowerCase());
    }
    return object;
  }

  @override
  Object? afterSerialize(Object object, FullType specifiedType) {
    return object;
  }
}

final serializers = (Serializers().toBuilder()
  ..addPlugin(StandardJsonPlugin())
  ..addPlugin(LowercaseEmailSerializerPlugin())
).build();
```

In the above code, we create a custom `LowercaseEmailSerializerPlugin` class that implements the `SerializerPlugin` interface. We override the `beforeSerialize` method and lowercase the `emailAddress` property of the `UserModel` before serializing it.

Finally, we add the `LowercaseEmailSerializerPlugin` to the `Serializers` builder to use it during serialization.

## Conclusion

Transforming JSON data during serialization is a useful technique when working with Flutter and JSON. By leveraging the built_value package and custom serializers, we can easily perform transformations on JSON data before or after serialization.

In this blog post, we explored how to define a model class using built_value, generate serialization code, and transform JSON data during serialization. This technique gives us more control over the serialization process and allows us to adapt the data as needed.

#flutter #JSON #serialization #transformingJSON #FlutterSerialization