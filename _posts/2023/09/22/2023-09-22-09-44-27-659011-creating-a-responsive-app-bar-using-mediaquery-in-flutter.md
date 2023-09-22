---
layout: post
title: "Creating a responsive app bar using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [flutter, responsive]
comments: true
share: true
---

In this blog post, we will learn how to create a responsive app bar using the `MediaQuery` class in Flutter. The app bar is an important UI component that provides navigation and quick access to various actions within an app. By making the app bar responsive, we ensure that it adapts to different screen sizes and orientations.

## What is MediaQuery?

`MediaQuery` is a class in Flutter that provides access to various information about the current device or app configuration. It allows us to retrieve properties like screen size, orientation, and more. Using `MediaQuery`, we can make our app UI responsive and adapt to different device constraints.

## Steps to Create a Responsive App Bar using MediaQuery

### Step 1: Import the required dependencies

Before we begin, make sure you have Flutter installed and set up in your development environment. Import the following packages in your Flutter project's `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
```

### Step 2: Create the App Bar Widget

In your Flutter project, create a new file called `app_bar.dart` and define a new widget for the app bar. Here's an example:

```dart
import 'package:flutter/material.dart';

class MyAppBar extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      height: MediaQuery.of(context).size.height * 0.1,
      color: Colors.blue,
      child: Center(
        child: Text(
          "App Bar",
          style: TextStyle(
            fontSize: 20,
            fontWeight: FontWeight.bold,
            color: Colors.white,
          ),
        ),
      ),
    );
  }
}
```
In the `build` method, we use `MediaQuery.of(context).size.height` to get the device's screen height, and multiply it by `0.1` to set the app bar's height to 10% of the screen height. The rest of the code is just styling the app bar by setting the background color and text properties.

### Step 3: Implement the App Bar

To use the app bar in your app, simply import the `app_bar.dart` file and include the `MyAppBar` widget in your widget tree. Here's an example of how you can use it within the `build` method of your main screen:

```dart
import 'package:flutter/material.dart';
import 'app_bar.dart';

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: MyAppBar(),
      body: Center(
        child: Text("Welcome to My App"),
      ),
    );
  }
}

void main() {
  runApp(MyApp());
}
```

### Step 4: Run the App

Now, you can run your Flutter app and see the responsive app bar in action. It will adapt its height based on the screen size, providing a consistent user experience across different devices.

## Conclusion

In this blog post, we have learned how to create a responsive app bar using `MediaQuery` in Flutter. By leveraging the `MediaQuery` class, we can easily make our app UI adapt to different screen sizes and orientations, providing a consistent and user-friendly experience.

#flutter #responsive #appbar