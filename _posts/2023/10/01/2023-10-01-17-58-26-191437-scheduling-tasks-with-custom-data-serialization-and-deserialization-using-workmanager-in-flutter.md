---
layout: post
title: "Scheduling tasks with custom data serialization and deserialization using WorkManager in Flutter"
description: " "
date: 2023-10-01
tags: [WorkManager]
comments: true
share: true
---

In Flutter, performing heavy tasks in the background is crucial for providing a smooth user experience. One way to achieve this is by using the **WorkManager** library, which allows us to schedule and run background tasks in a controlled manner. In this blog post, we'll learn how to schedule tasks using WorkManager and handle custom data serialization and deserialization.

## What is WorkManager?

WorkManager is a powerful library provided by the Android Jetpack suite that allows you to schedule and run deferrable, asynchronous tasks even if the app is not running. It provides a simple API to handle tasks in the foreground or background, and it takes care of managing and executing them based on system conditions and constraints.

## Setting up WorkManager in Flutter

To integrate WorkManager into your Flutter project, you'll need to add the [workmanager](https://pub.dev/packages/workmanager) package to your `pubspec.yaml` file.

```dart
dependencies:
  workmanager: ^0.4.0
```

After adding the package, make sure to run `flutter pub get` to fetch the latest dependencies.

## Scheduling a task with custom data serialization

To schedule a task with WorkManager, you need to define a unique `tag` for each task and configure its execution interval, constraints, and input data. Let's start by scheduling a task and passing custom data to it.

```dart
void scheduleTask() {
  const taskTag = 'custom_task';
  
  final inputData = MyCustomData(
    username: 'John',
    age: 25,
  ).toJson();

  Workmanager.initialize(
    callbackDispatcher,
    isInDebugMode: true,
  );
  Workmanager.registerOneOffTask(
    taskTag,
    'customTask',
    inputData: inputData,
  );
}
```

In the above code, we define a unique `taskTag` for our task and create an instance of `MyCustomData`. We then convert the object to a JSON string using the `toJson()` method.

## Deserializing custom data in the background task

Next, we need to handle the background task and deserialize the custom data. Let's define the `callbackDispatcher` function where we'll handle the background task execution.

```dart
void callbackDispatcher() {
  Workmanager.executeTask((taskName, inputData) async {
    if (taskName == 'customTask') {
      final customData = MyCustomData.fromJson(inputData);
      // Perform your task with customData
      print(customData.username);
      print(customData.age);
    }

    return Future.value(true);
  });
}
```

In the `callbackDispatcher` function, we use the `executeTask` method to handle the `customTask` we scheduled earlier. Inside this function, we deserialize the custom data using the `fromJson()` method of `MyCustomData` and perform our desired task using the deserialized data.

## Handling custom data serialization and deserialization

To enable custom data serialization and deserialization, we need to make our `MyCustomData` class implement the `JsonSerializable` interface from the `json_annotation` package. Here's an example:

```dart
import 'package:json_annotation/json_annotation.dart';

part 'my_custom_data.g.dart';

@JsonSerializable()
class MyCustomData {
  final String username;
  final int age;

  MyCustomData({this.username, this.age});

  factory MyCustomData.fromJson(Map<String, dynamic> json) =>
      _$MyCustomDataFromJson(json);
  Map<String, dynamic> toJson() => _$MyCustomDataToJson(this);
}
```

To generate the required serialization and deserialization methods, we need to run the following command in the terminal:

```shell
flutter pub run build_runner build
```

This command generates the necessary code in `my_custom_data.g.dart`.

## Conclusion

WorkManager in Flutter provides a convenient way to schedule and execute background tasks in a controlled manner. By implementing custom data serialization and deserialization, you can pass complex data structures to your background tasks and perform operations on them. This ensures that your app remains responsive and provides a seamless user experience.

#Flutter #WorkManager