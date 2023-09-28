---
layout: post
title: "Building a responsive list view using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [responsivedesign]
comments: true
share: true
---

With the increasing usage of smartphones and various screen sizes, it's crucial to build applications that can adapt and provide the best user experience across different devices. In this blog post, we'll explore how to create a responsive list view in Flutter using the `MediaQuery` class.

## What is `MediaQuery`?

`MediaQuery` is a class in Flutter that provides information about the current media, such as the size and orientation of the device screen. It allows you to retrieve the dimensions and characteristics of the current device, which can be used to build responsive user interfaces.

## Step 1: Set Up the Flutter Project

First, let's create a new Flutter project by running the following command:

```bash
flutter create responsive_list_view
```
## Step 2: Add Dependencies

Next, open the `pubspec.yaml` file in the root of your project and add the following dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter
  cupertino_icons: ^1.0.2
```

Save the file and run `flutter pub get` to fetch the dependencies.

## Step 3: Create the List View

In the newly created `lib/main.dart` file, replace the default code with the following:

```dart
import 'package:flutter/material.dart';
  
void main() {
  runApp(MyApp());
}
  
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Responsive List View',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyListView(),
    );
  }
}
  
class MyListView extends StatefulWidget {
  @override
  _MyListViewState createState() => _MyListViewState();
}
  
class _MyListViewState extends State<MyListView> {
  @override
  Widget build(BuildContext context) {
    final deviceSize = MediaQuery.of(context).size;
  
    return Scaffold(
      appBar: AppBar(
        title: Text('Responsive List View'),
      ),
      body: ListView.builder(
        itemBuilder: (ctx, index) {
          return Container(
            height: deviceSize.width > 600 ? 200 : 100,
            color: index % 2 == 0 ? Colors.blue : Colors.green,
            child: Center(
              child: Text(
                'Item $index',
                style: TextStyle(
                  fontSize: deviceSize.width > 600 ? 24 : 16,
                  color: Colors.white,
                ),
              ),
            ),
          );
        },
      ),
    );
  }
}
```
In this code, we have created a basic Flutter application with a responsive list view. We use the `MediaQuery.of(context).size` property to get the size of the current device screen. Based on this value, we adjust the height and font size of the list items to make them responsive.

## Step 4: Run the Application

Run the application using the `flutter run` command and observe the list view adjust its height and font size based on the device screen size.

## Conclusion

In this tutorial, we learned how to build a responsive list view in Flutter using `MediaQuery`. By utilizing the `MediaQuery` class, we can create adaptive and user-friendly interfaces that seamlessly adjust to different device sizes and orientations. This allows us to provide a better user experience to our application users.

#flutter #responsivedesign