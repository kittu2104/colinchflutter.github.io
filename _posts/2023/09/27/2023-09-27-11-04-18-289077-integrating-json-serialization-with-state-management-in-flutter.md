---
layout: post
title: "Integrating JSON serialization with state management in Flutter"
description: " "
date: 2023-09-27
tags: [json, state]
comments: true
share: true
---

State management is an essential part of developing applications in Flutter. It allows us to handle and update the state of our application efficiently. One common scenario in app development is working with JSON data. In this blog post, we will explore how to integrate JSON serialization with state management in Flutter.

## Setting Up
To start, let's set up our Flutter project with a state management package. We'll use `provider` as an example in this blog post, but the concepts can be applied to other state management solutions like `Riverpod` or `GetX`.

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(
    ChangeNotifierProvider(
      create: (context) => DataProvider(),
      child: MyApp(),
    ),
  );
}

// Define the model class for our data
class DataModel {
  final String name;
  final int age;

  DataModel({required this.name, required this.age});

  factory DataModel.fromJson(Map<String, dynamic> json) {
    return DataModel(
      name: json['name'] as String,
      age: json['age'] as int,
    );
  }

  Map<String, dynamic> toJson() {
    return {
      'name': name,
      'age': age,
    };
  }
}

// Create a ChangeNotifier provider class to manage data
class DataProvider with ChangeNotifier {
  DataModel? _data;

  DataModel? get data => _data;

  void updateData(DataModel newData) {
    _data = newData;
    notifyListeners();
  }
}

// Define the UI of our app
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'JSON Serialization with State Management',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  final TextEditingController _nameController = TextEditingController();
  final TextEditingController _ageController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    final dataProvider = Provider.of<DataProvider>(context);
    return Scaffold(
      appBar: AppBar(
        title: Text('JSON Serialization with State Management'),
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: <Widget>[
            TextField(
              decoration: InputDecoration(labelText: 'Name'),
              controller: _nameController,
            ),
            TextField(
              decoration: InputDecoration(labelText: 'Age'),
              controller: _ageController,
            ),
            ElevatedButton(
              onPressed: () {
                final newData = DataModel(
                  name: _nameController.text,
                  age: int.parse(_ageController.text),
                );
                dataProvider.updateData(newData);
              },
              child: Text('Update Data'),
            ),
            Consumer<DataProvider>(
              builder: (context, dataProvider, child) {
                final data = dataProvider.data;
                return Text(
                  'Name: ${data?.name ?? 'N/A'}\nAge: ${data?.age ?? 'N/A'}',
                );
              },
            ),
          ],
        ),
      ),
    );
  }
}
```

## JSON Serialization
Now that we have our state management set up, we need to handle JSON serialization/deserialization for our data class `DataModel`. To achieve this, we can use the `json_annotation` package, which provides annotations and code generation for JSON serialization.

### Installing Packages
Add the following dependencies in your `pubspec.yaml` file:
```yaml
dependencies:
  flutter:
    sdk: flutter
  provider: ^6.0.1
  json_annotation: ^4.4.3

dev_dependencies:
  flutter_test:
    sdk: flutter
  build_runner: ^2.1.3
  json_serializable: ^5.0.2
```

### Generating Serialization Code
To generate the serialization code, we need to run the following command:
```shell
flutter pub run build_runner build --delete-conflicting-outputs
```

This generates the `data_model.g.dart` file, which contains the serialization code.

### Using Serialization Code
Update your `data_model.dart` file as follows:

```dart
import 'package:json_annotation/json_annotation.dart';

part 'data_model.g.dart'; // Generated code

@JsonSerializable()
class DataModel {
  @JsonKey(name: 'name')
  final String name;

  @JsonKey(name: 'age')
  final int age;

  DataModel({required this.name, required this.age});

  factory DataModel.fromJson(Map<String, dynamic> json) =>
      _$DataModelFromJson(json); // Generated code

  Map<String, dynamic> toJson() => _$DataModelToJson(this); // Generated code
}
```

By using the `@JsonSerializable()` annotation and specifying the field names with `@JsonKey()`, we leverage the generated code to automatically serialize and deserialize our `DataModel` class.

## Conclusion
In this blog post, we learned how to integrate JSON serialization with state management in Flutter. We set up a Flutter project with the `provider` package, created a data model class, and used the `json_annotation` package to generate serialization code. By combining state management and JSON serialization, we can efficiently handle and update JSON data in our Flutter applications.

#flutter #json #state-management