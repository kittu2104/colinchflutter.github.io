---
layout: post
title: "How to use GetX for state management in Flutter"
description: " "
date: 2023-09-29
tags: [GetX, StateManagement]
comments: true
share: true
---

State management is a crucial aspect of developing Flutter applications, as it helps manage the changes in data and UI as the application grows in complexity. GetX is a powerful state management library in Flutter that provides an intuitive and efficient way to handle state in your application.

In this tutorial, we will explore how to use GetX for state management in your Flutter app.

## Installing GetX

Before we can start using GetX, we need to add the `get` package to our `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  get: ^4.3.8
```

Once added, run `flutter pub get` to fetch the package.

## Setting Up GetX

To start using GetX for state management, we need to initialize it in our main application file. In the `lib` folder, locate the `main.dart` file and add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return GetMaterialApp(
      title: 'MyApp',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: HomeScreen(),
    );
  }
}
```

Here, we imported the required packages and wrapped our `MyApp` widget with `GetMaterialApp`. This sets up GetX in our application.

## Using GetX for State Management

Now that we have GetX set up, let's see how we can use it for state management. GetX follows an observable pattern to track changes in state.

### Creating an Observable

We can start by creating an observable object using the `GetX` package. An observable object is simply a regular Dart class that extends `GetxController` and contains the data we want to observe. Let's create an example observable object, `User`, that holds the user's name:

```dart
class User extends GetxController {
  RxString name = ''.obs;
  
  void changeName(String newName) {
    name.value = newName;
  }
}
```

In this example, we define the `User` class that extends `GetxController`, and use the `RxString` type provided by GetX to make the `name` variable observable. We also provide a method, `changeName`, to update the name.

### Accessing the Observable

To access an observable object, we use `Get.put()` to assign an instance of the object to a variable. We can then reference this variable to access the observable properties. Let's modify our `HomeScreen` widget to use the `User` object we created:

```dart
class HomeScreen extends StatelessWidget {
  final User user = Get.put(User());

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('GetX State Management'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Obx(() => Text('User Name: ${user.name.value}')),
            ElevatedButton(
              onPressed: () => user.changeName('John Doe'),
              child: Text('Change Name'),
            ),
          ],
        ),
      ),
    );
  }
}
```

In this example, we use `Get.put()` to create an instance of the `User` class and assign it to the `user` variable. We then use `Obx` widget provided by GetX to automatically update the UI whenever the `name` property of `User` changes. We also have a button that calls the `changeName` method to update the name.

### Conclusion

Using GetX for state management in your Flutter application offers a concise and efficient way to handle changes in your app's data and UI. By creating observable objects and accessing them using `Get.put()`, you can easily manage and update your app's state.

Remember to make use of the powerful features provided by GetX, such as reactive programming, dependency injection, and more, to further enhance your state management capabilities.

## #Flutter #GetX #StateManagement