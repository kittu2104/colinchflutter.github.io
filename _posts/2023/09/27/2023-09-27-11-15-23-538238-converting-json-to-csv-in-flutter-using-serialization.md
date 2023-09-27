---
layout: post
title: "Converting JSON to CSV in Flutter using serialization"
description: " "
date: 2023-09-27
tags: []
comments: true
share: true
---

Converting JSON (JavaScript Object Notation) data to CSV (Comma-Separated Values) format is a common task in many applications. In Flutter, we can achieve this using serialization.

Serialization is the process of converting objects or data structures into a format that can be stored or transmitted. Flutter provides a package called 'json_serializable', which simplifies the serialization and deserialization of JSON data.

To convert JSON to CSV in Flutter, follow these steps:

## Step 1: Add Dependencies

Open your `pubspec.yaml` file and add the following dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter

  # add json_serializable and csv packages
  json_annotation: ^4.4.2
  csv: ^4.3.1
```

Save the file and run `flutter pub get` to fetch the new dependencies.

## Step 2: Create the Model Class

Create a model class that represents the structure of your JSON data. Annotate the class and its properties with `@JsonSerializable` and `@JsonKey` respectively to enable JSON serialization.

```dart
import 'package:json_annotation/json_annotation.dart';

part 'your_model_class.g.dart';

@JsonSerializable()
class YourModelClass {
  @JsonKey(name: 'id')
  int id;

  @JsonKey(name: 'name')
  String name;

  // add more properties as needed

  YourModelClass({this.id, this.name});

  factory YourModelClass.fromJson(Map<String, dynamic> json) =>
      _$YourModelClassFromJson(json);

  Map<String, dynamic> toJson() => _$YourModelClassToJson(this);
}
```

Run the following command in your project root directory to generate the serialization code:

```
flutter pub run build_runner build
```

## Step 3: Convert JSON to CSV

Now, with your model class in place, you can easily convert JSON data to CSV format.

```dart
import 'dart:convert';
import 'package:csv/csv.dart';

void main() {
  String jsonEncodedData = '[{"id": 1, "name": "John"}, {"id": 2, "name": "Jane"}]';

  // Decode JSON data
  List<dynamic> jsonData = jsonDecode(jsonEncodedData);

  // Convert JSON to models
  List<YourModelClass> models = jsonData.map((json) => YourModelClass.fromJson(json)).toList();

  // Convert models to CSV rows
  List<List<dynamic>> csvData = [];
  csvData.add(['ID', 'Name']); // Add header row
  models.forEach((model) {
    csvData.add([model.id, model.name]);
  });

  // Convert CSV rows to CSV format
  String csvString = const ListToCsvConverter().convert(csvData);

  print(csvString);
}
```

In the above example, we decode the JSON data using `jsonDecode`, convert the decoded JSON to a list of models using the `fromJson` factory method, and then we convert the model list to CSV rows. Finally, we convert the CSV rows to a CSV string using `ListToCsvConverter`.

## Step 4: Process the CSV Data

At this point, you have the CSV data in a `String` format. You can choose to save it to a file, send it as an attachment, or process it further.

```dart
// ...
// Step 3 code...

// Example: Save CSV data to a file
final directory = await getApplicationDocumentsDirectory();
final file = File('${directory.path}/data.csv');
await file.writeAsString(csvString);

print('CSV file saved to: ${file.path}');
```

This example shows how to save the CSV data as a file. You can change the file path as needed. Remember to include the necessary import statements at the top of your Dart file.

## Conclusion

By utilizing serialization in Flutter, converting JSON data to CSV format becomes a straightforward process. The `json_serializable` package makes it easy to convert JSON to models, and the `csv` package enables easy manipulation and processing of CSV data.