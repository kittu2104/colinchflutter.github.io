---
layout: post
title: "Storing JSON data in local storage with Flutter"
description: " "
date: 2023-09-27
tags: [json]
comments: true
share: true
---

In Flutter, it is common to need to store data locally on the device. One common use case is storing JSON data, which is a lightweight and widely used data format. In this article, we'll explore how to store JSON data in local storage using the shared_preferences package in Flutter.

## Installing the shared_preferences package

To get started, you need to add the shared_preferences package as a dependency in your Flutter project. Include the following line in your `pubspec.yaml` file:

```yaml
dependencies:
  shared_preferences: ^2.0.6
```
*#flutter *#json

Make sure to run `flutter pub get` to fetch the package and its dependencies.

## Storing JSON data

1. Import the necessary packages:

```dart
import 'package:shared_preferences/shared_preferences.dart';
import 'dart:convert';
```

2. Define a function to store the JSON data in local storage:

```dart
void storeJsonData(Map<String, dynamic> jsonData) async {
  SharedPreferences preferences = await SharedPreferences.getInstance();
  String jsonString = jsonEncode(jsonData);
  await preferences.setString('json_data', jsonString);
  print('JSON data stored successfully!');
}
```

3. Use the `storeJsonData` function to store your JSON data:

```dart
Map<String, dynamic> jsonData = {
  'name': 'John Doe',
  'age': 25,
  'email': 'johndoe@example.com',
};

storeJsonData(jsonData);
```

## Retrieving JSON data

To retrieve the stored JSON data, follow these steps:

1. Define a function to retrieve the JSON data from local storage:

```dart
Map<String, dynamic> retrieveJsonData() {
  SharedPreferences preferences = await SharedPreferences.getInstance();
  String jsonString = preferences.getString('json_data');
  Map<String, dynamic> jsonData = jsonDecode(jsonString);
  return jsonData;
}
```

2. Call the `retrieveJsonData` function to get the stored JSON data:

```dart
Map<String, dynamic> storedData = retrieveJsonData();
print('Retrieved JSON data: $storedData');
```

That's it! You have successfully stored and retrieved JSON data using local storage in Flutter.

## Conclusion

Storing JSON data in local storage can be a useful way to persist data within your Flutter applications. By following the steps outlined in this article, you can easily store and retrieve JSON data using the shared_preferences package. Happy coding!

*#Flutter *#localstorage