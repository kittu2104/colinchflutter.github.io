---
layout: post
title: "Converting JSON to XML in Flutter using serialization"
description: " "
date: 2023-09-27
tags: [JSONtoXML]
comments: true
share: true
---

In mobile app development using Flutter, it is common to work with different data formats such as JSON and XML. Flutter provides a powerful serialization library called `json_serializable` which makes it easy to convert JSON data into Dart objects. However, there are times when we need to convert JSON data into XML format for specific requirements. In this blog post, we will explore how to convert JSON to XML in Flutter using serialization.

## Step 1: Add Dependencies

First, we need to add the necessary dependencies to our `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  json_serializable: ^5.0.2
  xml: ^5.0.0
```

Make sure to run `flutter pub get` command in your terminal to install the dependencies.

## Step 2: Create Model Classes

Next, let's create the model classes for JSON serialization and XML conversion. We will use the `json_annotation` package along with the `xml` package for this.

```dart
import 'package:json_annotation/json_annotation.dart';
import 'package:xml/xml.dart' as xml;

part 'person.g.dart'; // Generated file

@JsonSerializable()
class Person {
  final String name;
  final int age;

  Person({required this.name, required this.age});

  factory Person.fromJson(Map<String, dynamic> json) =>
      _$PersonFromJson(json);

  Map<String, dynamic> toJson() => _$PersonToJson(this);

  xml.XmlElement toXml() {
    final builder = xml.XmlBuilder();
    builder.element('person', nest: () {
      builder.element('name', nest: name);
      builder.element('age', nest: age.toString());
    });
    return builder.build();
  }
}
```

The `Person` class represents our JSON object. It has the necessary annotations for JSON serialization and methods to convert the object to XML using the `xml` package.

## Step 3: Generate Serialization Code

To generate the serialization code, run the following command in your terminal:

```bash
flutter pub run build_runner build
```

This will generate the serialization code for your model classes.

## Step 4: Convert JSON to XML

Now we are ready to convert our JSON data to XML format using the model classes we created. Here is an example:

```dart
import 'dart:convert';
import 'package:xml/xml.dart' as xml;

void main() {
  final jsonData = '{"name": "John Doe", "age": 25}';
  final jsonMap = json.decode(jsonData);
  final person = Person.fromJson(jsonMap);
  final xmlElement = person.toXml();
  final xmlString = xmlElement.toXmlString(pretty: true);

  print(xmlString);
}
```

In the above example, we parse the JSON data, create a `Person` object using the generated code, and then convert it into an XML element. Finally, we convert the XML element to a string representation.

## Conclusion

In this blog post, we learned how to convert JSON data to XML format in Flutter using serialization. By leveraging the `json_serializable` and `xml` packages, we can easily handle data conversion between different formats. This can be particularly useful when working with APIs or when specific XML requirements are needed. Give it a try and experiment with different JSON objects and XML structures in your Flutter projects.

#flutter #JSONtoXML